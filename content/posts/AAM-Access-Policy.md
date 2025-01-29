---
title: "AAM Access Policy"
description: "You can refer to table of contents for the AAM Access Policy with the stacks that is relevant.
"
date: 2025-01-28
# image: ""
lastmod: 2025-01-29
showTableOfContents: true
tags: ["wordpress",]
type: "post"
---

## ACCSS, Frames, JetEngine, Bricks

{{< collapsible "Click to expand" >}}

```json
{
    "Version": "1.0.0",
    "Dependency": {
        "wordpress": ">=6.7.1",
        "advanced-access-manager": ">=6.9.45"
    },
    "Statement": [
        {
            "Effect": "deny",
            "Resource": [
                "BackendMenu:update-core.php",
                "BackendMenu:bricks-system-information",
                "BackendMenu:bricks-license",
                "BackendMenu:bricks-sidebars",
                "BackendMenu:bricks",
                "BackendMenu:bricks-settings",
                "BackendMenu:edit.php?post_type=bricks_template",
                "BackendMenu:menu-bricks",
                "BackendMenu:menu-edit.php?post_type=page",
                "BackendMenu:menu-edit-comments.php",
                "BackendMenu:menu-jet-dashboard",
                "BackendMenu:menu-jet-engine",
                "BackendMenu:menu-themes.php",
                "BackendMenu:plugin-install.php",
                "BackendMenu:plugin-editor.php",
                "BackendMenu:plugins.php",
                "BackendMenu:menu-plugins.php",
                "BackendMenu:menu-options-general.php",
                "BackendMenu:menu-automatic-css",
                "BackendMenu:menu-frames",
                "BackendMenu:menu-aam"
            ]
        },
        {
            "Effect": "deny",
            "Resource": [
                "Toolbar:toolbar-wp-logo",
                "Toolbar:aam",
                "Toolbar:toolbar-comments",
                "Toolbar:toolbar-automatic-css-admin-bar"
            ]
        },
        {
            "Effect": "allow",
            "Resource": [
                "Capability:switch_themes",
                "Capability:edit_themes",
                "Capability:activate_plugins",
                "Capability:edit_plugins",
                "Capability:edit_users",
                "Capability:edit_files",
                "Capability:manage_options",
                "Capability:moderate_comments",
                "Capability:manage_links",
                "Capability:upload_files",
                "Capability:import",
                "Capability:unfiltered_html",
                "Capability:edit_posts",
                "Capability:edit_others_posts",
                "Capability:edit_published_posts",
                "Capability:publish_posts",
                "Capability:edit_pages",
                "Capability:read",
                "Capability:level_10",
                "Capability:level_9",
                "Capability:level_8",
                "Capability:level_7",
                "Capability:level_6",
                "Capability:level_5",
                "Capability:level_4",
                "Capability:level_3",
                "Capability:level_2",
                "Capability:level_1",
                "Capability:level_0",
                "Capability:edit_others_pages",
                "Capability:edit_published_pages",
                "Capability:publish_pages",
                "Capability:delete_pages",
                "Capability:delete_others_pages",
                "Capability:delete_published_pages",
                "Capability:delete_posts",
                "Capability:delete_others_posts",
                "Capability:delete_published_posts",
                "Capability:delete_private_posts",
                "Capability:edit_private_posts",
                "Capability:read_private_posts",
                "Capability:delete_private_pages",
                "Capability:edit_private_pages",
                "Capability:read_private_pages",
                "Capability:delete_users",
                "Capability:create_users",
                "Capability:unfiltered_upload",
                "Capability:edit_dashboard",
                "Capability:update_plugins",
                "Capability:delete_plugins",
                "Capability:install_plugins",
                "Capability:update_themes",
                "Capability:install_themes",
                "Capability:update_core",
                "Capability:list_users",
                "Capability:remove_users",
                "Capability:promote_users",
                "Capability:edit_theme_options",
                "Capability:delete_themes",
                "Capability:export",
                "Capability:bricks_upload_svg",
                "Capability:bricks_form_submission_access",
                "Capability:bricks_execute_code",
                "Capability:manage_taxonomy",
                "Capability:manage_category",
                "Capability:administrator"
            ]
        }
    ],
    "Param": [
        {
            "Key": "redirect:on:access-denied:frontend",
            "Value": {
                "Type": "message",
                "Message": "Access denied.\\n\\nThis is usually where the technical Zone is implemented and introduces the risk of miss-clicks, miss-configuration that could break the site.\\n\\nContact kevin@berlime.com if you need help."
            }
        }
    ]
}
```
{{< /collapsible >}}
> - *Post Changelogs*
>   - *Nothing Yet*
