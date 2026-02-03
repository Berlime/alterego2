---
title: "Bricks + Brevo integration"
description: "Step-by-step: send Bricks form submissions to Brevo (Sendinblue) and how to edit functions.php in Hostinger"
date: 2026-02-03
lastmod: 2026-02-03
type: "post"
showTableOfContents: true
tags: ["WordPress", "bricks", "Brevo"]
---

This post walks through sending Bricks Builder form submissions to Brevo (Sendinblue) so new contacts land in a list. The code below uses the current Bricks hook and Brevo API; the [video tutorial](https://youtu.be/i6pAc0U4j9M?si=vTPw865cKUjsLyu2) uses older code. For the same approach with more context (registration required), see the author’s article: [How to create subscription list using Brevo API and Bricks Builder form element](https://mangwp.com/how-to-create-subscription-list-using-brevo-api-and-bricks-builder-form-element/).

## Prerequisites

- WordPress (this guide uses Hostinger; steps for editing `functions.php` are Hostinger-specific).
- Bricks Builder with a form on the front end.
- Brevo (Sendinblue) account: you’ll need an API key and at least one list ID.

## Brevo setup

1. In Brevo, create or open the list you want contacts in; note the **list ID** (e.g. `5`). You’ll see it in the list URL or in list settings.
2. Create an **API key**: Brevo → **Settings** → **API Keys** (SMTP & API or API-only is fine).
3. Ensure contact attributes exist and **names match the code exactly** (e.g. `FIRSTNAME`, `SMS`). Brevo attribute names are case-sensitive. Create them under **Contacts** → **Settings** → **Contact attributes** if needed.

## Bricks form setup

1. Add a **Form** element in Bricks and add fields (e.g. email, phone, first name).
2. In the form’s settings, set **Action** to **Custom** so Bricks fires the `bricks/form/custom_action` hook.
3. Note your **Form ID** and each field’s **field key**:
   - **Form ID**: In the Form element’s settings (or in the markup), you’ll see an ID like `cefkbt`. You’ll use this in the code to target this form only.
   - **Field keys**: Each form field has a unique key (e.g. `form-field-23e3bb`, `form-field-olqpbb`). In Bricks, select the field and check the **Name** or the generated HTML `name` attribute in the builder; the value is the field key you’ll use in PHP.

## Hostinger: open and edit `functions.php`

1. Log in to **hPanel** → select your hosting plan → **Manage** → **File Manager** (or go via **Files** → **File Manager**).
2. In File Manager, go to: **public_html** → **wp-content** → **themes** → **your active theme folder**. If you use a child theme, open the **child theme** folder so updates to the parent theme don’t overwrite your code.
3. Locate **functions.php**. Create a backup first: right-click → **Copy** (and rename the copy) or download the file.
4. Open **functions.php**: double-click the file or right-click → **Edit**. Hostinger’s File Editor opens with syntax highlighting.
5. Add the code block from the next section at the **end** of `functions.php` (before a closing `?>` if your file has one, or simply at the very end; WordPress does not require `?>`).
6. Save with the editor’s **Save** button (or Ctrl+S). If you use a caching plugin, clear cache after saving.

Reference: [How to use the File Editor at Hostinger](https://support.hostinger.com/en/articles/7949267-how-to-use-the-file-editor-at-hostinger).

## Code: what to add

Customize the following before pasting:

- Replace `'cefkbt'` with your Bricks Form ID.
- Replace `form-field-23e3bb`, `form-field-olqpbb`, `form-field-hzjoep` with your Bricks field keys (email, phone, first name).
- Replace `'xxxxxxxxxx'` with your Brevo API key.
- Replace `array(5)` in `listIds` with your Brevo list ID(s), e.g. `array(5, 12)` for multiple lists.
- Ensure Brevo attribute names in the code (`FIRSTNAME`, `SMS`) match your Brevo contact attributes exactly.

Full code (copy into `functions.php`):

{{< collapsible "Full code (copy into functions.php)" >}}
```php
function wp_form_save_to_cpt($form)
{
    // Retrieve all the fields from the form submission
    $fields = $form->get_fields();

    // Extract the Bricks Form ID from the form fields
    $formId = $fields['formId'];

    // Check if the form ID matches 'cefkbt' (replace with your form ID)
    if ($formId == 'cefkbt') {
        // Retrieve the field values (replace field keys with your actual keys)
        $email = isset($fields['form-field-23e3bb']) ? $fields['form-field-23e3bb'] : '';
        $phone = isset($fields['form-field-olqpbb']) ? $fields['form-field-olqpbb'] : '';
        $fname = isset($fields['form-field-hzjoep']) ? $fields['form-field-hzjoep'] : '';

        // Proceed if the email is not empty
        if (!empty($email)) {
            // API URL for Brevo (Sendinblue) Contact creation
            $api_url = 'https://api.brevo.com/v3/contacts';

            // API Key for Brevo (replace 'YOUR_API_KEY' with your actual API key)
            $api_key = 'xxxxxxxxxx';

            // Ensure attribute keys match Brevo custom attributes exactly
            $data = array(
                'email' => $email,
                'attributes' => array(
                    'FIRSTNAME' => $fname, // Must match Brevo attribute name
                    'SMS' => $phone, // Must match Brevo attribute name
                ),
                'listIds' => array(5), // Replace with your actual list ID
            );

            // Debug: Log payload before sending
            error_log('Brevo payload: ' . print_r($data, true));

            // Send data to Brevo using wp_remote_post
            $response = wp_remote_post($api_url, array(
                'method'    => 'POST',
                'headers'   => array(
                    'Content-Type'  => 'application/json',
                    'api-key'       => $api_key,
                ),
                'body'      => json_encode($data),
                'timeout'   => 45,
            ));

            // Handle response
            if (is_wp_error($response)) {
                // Log error if needed
                error_log('Brevo API Error: ' . $response->get_error_message());
            } else {
                $response_body = wp_remote_retrieve_body($response);
                $result = json_decode($response_body);

                // Debug: Log Brevo response
                error_log('Brevo API Response: ' . $response_body);

                if (isset($result->id)) {
                    // Success: Contact created
                    error_log('Contact successfully added to Brevo with ID: ' . $result->id);
                } else {
                    // Failed to create contact
                    error_log('Brevo API Response Error: ' . $response_body);
                }
            }
        }
    }
}

add_action('bricks/form/custom_action', 'wp_form_save_to_cpt', 10, 1);
```
{{< /collapsible >}}

If you edit the active theme’s `functions.php` directly, use a **child theme** for this code so parent theme updates don’t overwrite it.

## Testing and troubleshooting

1. Submit the Bricks form on the front end; check **Brevo → Contacts** (and the list) for the new contact.
2. The code uses `error_log()` for debugging. On Hostinger you can check logs in **Advanced** → **Error logs** (or the path shown in hPanel). Look for lines like `Brevo payload:` and `Brevo API Response:` to verify the request and Brevo’s reply.
3. If the hook or Bricks API changes in a future Bricks version, check [Bricks documentation](https://academy.bricksbuilder.io/) or the [mangwp.com article](https://mangwp.com/how-to-create-subscription-list-using-brevo-api-and-bricks-builder-form-element/) for the latest hook name and usage.

## References

- [Video: Bricks + Brevo (code in video is outdated)](https://youtu.be/i6pAc0U4j9M?si=vTPw865cKUjsLyu2)
- [mangwp.com: Subscription list with Brevo API and Bricks form](https://mangwp.com/how-to-create-subscription-list-using-brevo-api-and-bricks-builder-form-element/) (registration required)
- [Hostinger: How to use the File Editor](https://support.hostinger.com/en/articles/7949267-how-to-use-the-file-editor-at-hostinger)
