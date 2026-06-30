# Service Portal — Theming & OOTB Reference

Source: ServiceNow SDK reference guide and community docs.

## SCSS Variables — Always Available (Bootstrap/SP Defaults)

```scss
$border-radius-base   $border-radius-large   $border-radius-small
$font-size-base       $font-size-small       $font-size-large
$btn-primary-color    $panel-primary-text    $link-color
$state-success-bg     $state-warning-bg      $state-danger-bg     $state-info-bg
$alert-success-border $alert-warning-border  $alert-danger-border $alert-info-border
$body-bg              $component-active-bg   $btn-default-border
$panel-border-color   $input-border          $input-border-focus
```

## Coral Theme Variables

### Backgrounds

| Variable | Use Case |
|----------|----------|
| `$background-primary` | Card / surface background |
| `$sp-page-bg` | Page background |
| `$background-secondary` | Subtle / muted background |
| `$background-tertiary` | Heavier subtle background |
| `$sp-form-field--background-color` | Input field background |

### Borders

| Variable | Use Case |
|----------|----------|
| `$border-tertiary` | Default border (cards, dividers) |
| `$border-secondary` | Medium emphasis border |
| `$border-primary` | Strong emphasis border |

### Text

| Variable | Use Case |
|----------|----------|
| `$text-color` | Primary text |
| `$text-secondary` | Secondary text |
| `$text-muted` | Muted / helper text |
| `$btn-primary-color` | White text on dark backgrounds |

### Brand Colors

| Variable | Use Case |
|----------|----------|
| `$brand-primary` | Primary brand |
| `$brand-primary-dark` | Primary dark (hover) |
| `$brand-primary-lighter` | Primary lighter (highlights) |
| `$brand-success` | Success |
| `$brand-warning` | Warning |
| `$brand-danger` | Danger |
| `$brand-info` | Info |
| `$link-color` | Link color |

## Spacing Scale

Use only these values — never arbitrary pixel values.

| Variable | Value | Use Case |
|----------|-------|----------|
| `$sp-space-1` | 4px | Icon gaps, badge padding |
| `$sp-space-2` | 8px | Input padding, label gaps |
| `$sp-space-3` | 12px | Button padding Y, tight sections |
| `$sp-space-4` | 16px | **Base unit** — form group gap |
| `$sp-space-5` | 24px | Card padding, section gap |
| `$sp-space-6` | 32px | Between major sections |
| `$sp-space-7` | 48px | Page top padding, empty states |
| `$sp-space-8` | 64px | Full-bleed sections |

## Typography Scale

Every `font-size` must use a theme variable — never a raw pixel value.

| Variable | Value | Use Case |
|----------|-------|----------|
| `$sp-text-xs` | 12px | Badges, timestamps, captions |
| `$sp-text-sm` | 14px | Helper text, table metadata |
| `$sp-text-base` | 16px | Body, labels, table cells |
| `$sp-text-md` | 18px | Card titles, sub-headings |
| `$sp-text-lg` | 22px | Section headings |
| `$sp-text-xl` | 26px | Page title |
| `$sp-text-2xl` | 32px | Hero / banner headings |

## Icon Size Scale

| Variable | Value | Use Case |
|----------|-------|----------|
| `$sp-icon-xs` | 12px | Badge / chevron icons |
| `$sp-icon-sm` | 16px | Button / inline / alert icons |
| `$sp-icon-md` | 20px | Card / stat tile icons |
| `$sp-icon-lg` | 32px | Section / feature icons |
| `$sp-icon-xl` | 48px | Empty state / hero icons |

## Bootstrap Grid Patterns

| Layout | Classes |
|--------|---------|
| Full-width | `col-md-12` |
| Main + sidebar | `col-md-8` + `col-md-4` |
| Equal 2-column | `col-md-6 col-xs-12` x 2 |
| 3-column cards | `col-md-4 col-sm-6 col-xs-12` x 3 |
| 4-column stat tiles | `col-md-3 col-sm-6 col-xs-12` x 4 |

Always add `col-xs-12` — every column must stack on mobile.

## CSS Anti-Patterns

| Anti-Pattern | Correct |
|--------------|---------|
| `style=""` inline | Use SCSS class |
| Raw hex values | Use `$brand-primary`, `$text-color`, etc. |
| `<br>` for spacing | Use margin/padding utilities |
| `!important` in widget CSS | Increase selector specificity |
| Input without `<label>` | Every input paired with label + matching `id` |
| `ng-repeat` without `track by` | Always `track by item.sys_id` |
| Missing `type` on `<button>` | Always `type="button"` or `type="submit"` |
| `GlideRecord` without `setLimit()` | Always `setLimit(n)` |

## OOTB Widgets

Reuse these before creating custom widgets.

| Name | Widget ID | Use Case |
|------|-----------|----------|
| Data Table | `widget-data-table` | Record list/table views |
| Form | `widget-form` | Full ServiceNow form |
| Typeahead Search | `typeahead-search` | Search with autocomplete |
| Faceted Search | `faceted_search` | Filtered search results |
| Login | `widget-login` | Portal login form |
| User Profile | `user-profile` | User profile card |
| Ticket Conversations | `widget-ticket-conversation` | Activity stream |
| Ticket Attachments | `widget-ticket-attachments` | File upload/attachment list |
| Breadcrumbs | `breadcrumbs` | Navigation breadcrumb trail |
| Simple List | `widget-simple-list` | Minimal record list |

## OOTB Pages

| Title | Page ID | Use Case |
|-------|---------|----------|
| Form | `form` | Generic record form |
| List | `list` | Generic record list |
| Ticket Form | `ticket` | Ticket/case detail |
| Login | `login` | Portal login |
| Not Found | `404` | 404 error page |
| Search | `search` | Search results |
| Approvals | `approvals` | Approval list |
| My Requests | `requests` | User's requests |
| User Profile | `user_profile` | User profile |
| Catalog Home (v2) | `sc_landing` | Service Catalog landing |
| Catalog Item | `sc_cat_item` | Catalog item order form |
| KB View | `kb_view` | Knowledge base home |
| KB Article | `kb_article` | Knowledge article reader |

## Menu Item Types (sp_instance_menu)

| Type | Fields | Description |
|------|--------|-------------|
| `page` | `page` (required) | Links to an SP page |
| `url` | `url`, `urlTarget` | External or internal URL |
| `sc` | (none) | Service Catalog home |
| `sc_category` | `scCategory`, `page` | Catalog category |
| `sc_cat_item` | `catItem`, `page` | Specific catalog item |
| `kb` | (none) | Knowledge Base home |
| `kb_topic` | `kbTopic`, `page` | Knowledge topic |
| `kb_article` | `kbArticle`, `page` | Specific KB article |
| `kb_category` | `kbCategory`, `page` | Knowledge category |
| `filtered` | `table`, `filter`, display fields | Dynamic content based on filter |
| `scripted` | `script` | Server-side generated items |

## Troubleshooting

### Portal not accessible
- Verify `urlSuffix` is unique and doesn't conflict with other portals
- Check user has access permissions

### Theme not applying
- Confirm theme is linked to portal (`sp_portal.theme`)
- Check SCSS compilation errors in browser console

### Navigation menu not showing
- Verify portal has `theme` configured
- Verify theme has `header` configured
- Verify portal has `mainMenu` configured

### Widget not displaying
- Check widget is active (`sp_widget` table)
- Verify page/instance configuration
- Check browser console for JS errors

### Data not updating in widget
- Verify server script IIFE syntax is correct
- Check `c.server.get()` / `c.server.update()` calls match `input.action` handling

### Styling issues
- Use SCSS token variables (not raw hex)
- Check Bootstrap 3 class names (not Bootstrap 4/5)
- Confirm SCSS compilation is enabled on theme

### Library not loading
- Verify CDN URL is accessible from the instance network
- Check dependency `order` values — base libs first, plugins after
- Confirm dependency is linked to widget

### Provider not available
- Verify provider is injected in the widget's angular provider list
- Check function name matches the provider name exactly
- Verify script syntax is valid
