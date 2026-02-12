# HTML Email Template Notes

## Email Client Limitations

### Why Table-Based Layouts?

Email clients have inconsistent CSS support compared to modern web browsers. Many email clients strip out `<style>` tags, ignore external stylesheets, and have poor support for modern CSS features like Flexbox and Grid. Table-based layouts are the most reliable way to ensure consistent rendering across different email clients.

### Key Email Client Constraints

#### 1. **CSS Support Limitations**
- **Inline CSS Only**: Most email clients strip `<style>` tags and external stylesheets. All CSS must be inline using the `style` attribute.
- **Limited CSS Properties**: Many CSS3 properties are not supported (e.g., `position`, `float`, `flexbox`, `grid`, `transforms`, `animations`).
- **No JavaScript**: JavaScript is completely blocked in email clients for security reasons.
- **No External Resources**: External images should use absolute URLs, but external fonts and stylesheets are generally not supported.

#### 2. **Major Email Clients & Their Quirks**

##### Outlook (Windows Desktop - using Word rendering engine)
- **Most Restrictive**: Uses Microsoft Word's HTML rendering engine (not a web browser)
- Does not support `background-image`, `margin`, `padding` on various elements
- Poor support for `border-radius`, `box-shadow`
- Requires VML (Vector Markup Language) for advanced features
- Max width should be ~600px for reliable rendering

##### Gmail
- Strips `<style>` tags in the `<head>`
- Supports most inline CSS
- Converts some styles to classes
- Clips messages over 102KB

##### Apple Mail / iOS Mail
- Best CSS support among email clients
- Supports most modern CSS properties
- Handles responsive design well

##### Outlook.com / Hotmail
- Better than desktop Outlook but still limited
- Supports some CSS3 properties
- Inconsistent `margin` and `padding` support

##### Yahoo Mail
- Limited CSS support
- Strips some inline styles
- Poor handling of responsive design

#### 3. **Best Practices for Email HTML**

##### Structure
- Use `<table>` for layout structure
- Use nested tables for complex layouts
- Set `cellpadding="0"` and `cellspacing="0"` on all tables
- Use `border="0"` to remove default table borders
- Always declare width explicitly on table cells

##### Dimensions
- Maximum width of 600px for optimal desktop and mobile viewing
- Use pixels (px) rather than percentages for widths in older email clients
- Set explicit heights where needed

##### Colors
- Use full 6-character hex codes (#FFFFFF) instead of shorthand (#FFF)
- Always specify both `background-color` and `color`
- Use `bgcolor` attribute as fallback for background colors on `<table>` and `<td>`

##### Images
- Use absolute URLs (https://) for all image sources
- Always include `alt` text for accessibility
- Set explicit `width` and `height` attributes
- Use `display: block;` on images to remove unwanted spacing
- Use `border="0"` to remove default borders in Outlook

##### Fonts
- Stick to web-safe fonts: Arial, Helvetica, Georgia, Times New Roman, Courier
- Use font stacks as fallbacks: `font-family: Arial, Helvetica, sans-serif;`
- Web fonts (Google Fonts) have limited support - use with fallbacks

##### Spacing
- Use `padding` on `<td>` elements for spacing (better support than margin)
- Use empty `<td>` cells or spacer images for precise spacing
- Avoid `margin` - it's unreliable in email clients

##### Links
- Always use absolute URLs (https://)
- Include `color` style on links as inline CSS
- Consider using `text-decoration: underline;` explicitly

#### 4. **Responsive Design**

While many modern email clients support media queries, they should be used as progressive enhancement:
- Place media queries in `<style>` tags in the `<head>`
- Use `!important` to override inline styles in media queries
- Provide a solid baseline experience without media queries
- Target viewport width of 600px as the breakpoint

#### 5. **Testing Recommendations**

Always test emails in multiple clients:
- Outlook 2016/2019/365 (Windows)
- Gmail (web, iOS, Android)
- Apple Mail (macOS, iOS)
- Outlook.com
- Yahoo Mail
- Thunderbird

Use testing services like Litmus or Email on Acid for comprehensive testing across devices and clients.

#### 6. **Common Pitfalls to Avoid**

- Don't use background images (especially in Outlook)
- Don't use `div` for layout - use `table` instead
- Don't rely on `class` or `id` selectors - use inline styles
- Don't use complex CSS selectors
- Don't forget to test on actual devices
- Don't exceed 102KB total file size (Gmail clipping)
- Don't use form elements - they're often stripped
- Don't use video or audio elements

#### 7. **Accessibility Considerations**

- Use semantic HTML where possible
- Include `alt` text on all images
- Use sufficient color contrast (WCAG AA: 4.5:1 for normal text)
- Use `role="presentation"` on layout tables
- Provide text version as alternative
- Ensure readable font sizes (minimum 14px)

## Template Structure

All templates in this repository follow these principles:
1. Centered 600px width container table
2. Inline CSS for all styling
3. Table-based layout structure
4. Web-safe fonts with fallbacks
5. Full 6-character hex color codes
6. Absolute URLs for any external resources
7. Explicit dimensions on all tables and cells
8. Fallback `bgcolor` attributes alongside CSS background colors
