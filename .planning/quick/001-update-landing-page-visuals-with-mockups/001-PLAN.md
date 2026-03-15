---
task: 001-update-landing-page-visuals-with-mockups
type: quick
description: Update landing page visuals with proper mockup screenshots per TT-1
files_modified:
  - assets/images/hero-laptop.png
  - assets/images/hero-iphone.png
  - assets/images/problem-excel.png
  - assets/images/problem-whatsapp.png
  - assets/images/features-notification.png
  - index.html
autonomous: false
---

<objective>
Generate realistic device mockups for the TeamTigrr landing page using Nano Banana Pro, then integrate them into the existing HTML sections.

Purpose: Replace CSS-simulated UI elements with proper visual mockups showing real app/tool screenshots
Output: 5 generated images placed in assets/images/, index.html updated to use them
</objective>

<context>
@index.html
</context>

<tasks>

<task type="auto">
  <name>Task 1: Generate Hero Laptop Mockup</name>
  <files>assets/images/hero-laptop.png</files>
  <action>
Use /nano-banana skill to generate a laptop mockup image.

Prompt for generation:
"MacBook Pro laptop mockup showing a web app dashboard. The screen displays a sports team duty management interface with:
- Header: 'Tigers U12 Season Schedule'
- Table view with columns: Date, Game, Location, Game Clock (assigned name), Scoreboard (assigned name), Shot Clock (assigned name)
- Several rows of upcoming games with green checkmarks for filled duties
- Clean, modern SaaS dashboard aesthetic with dark sidebar navigation
- Orange accent color (#FF6B00) for highlights and buttons
Professional product photography style, 3/4 angle view, soft gradient background"

Save output to assets/images/hero-laptop.png
  </action>
  <verify>File exists at assets/images/hero-laptop.png, image shows laptop with dashboard</verify>
  <done>Laptop mockup generated showing team leader's schedule view</done>
</task>

<task type="auto">
  <name>Task 2: Generate Hero iPhone Mockup</name>
  <files>assets/images/hero-iphone.png</files>
  <action>
Use /nano-banana skill to generate an iPhone mockup image.

Prompt for generation:
"iPhone 14 Pro mockup showing a mobile app screen. The app displays:
- A list of upcoming basketball games with assigned duties
- Each game shows: date, opponent, venue, and duty assignments
- Push notification overlay at top: 'Reminder: Scoreboard task this Saturday March 6th at 16:30'
- Clean mobile UI with orange accent color (#FF6B00)
- Dark theme interface matching TeamTigrr brand
Professional product photography, front view with slight tilt, soft shadow"

Save output to assets/images/hero-iphone.png
  </action>
  <verify>File exists at assets/images/hero-iphone.png, shows iPhone with app and notification</verify>
  <done>iPhone mockup generated showing parent's games view with reminder notification</done>
</task>

<task type="auto">
  <name>Task 3: Generate Problem Section Excel Mockup</name>
  <files>assets/images/problem-excel.png</files>
  <action>
Use /nano-banana skill to generate an Excel spreadsheet mockup.

Prompt for generation:
"Microsoft Excel spreadsheet screenshot showing a messy duty roster. The spreadsheet contains:
- Filename tab: 'Roster_U12_Final_v3_copy.xlsx'
- Columns: Game Date, Time, Location (Court 1, Court 2), Game Clock, Scoreboard, 24-sec Shot Clock
- Multiple rows with game entries
- Some cells have names, others have '???' or are empty (showing unfilled duties)
- Highlighted cells in yellow or red indicating problems
- Typical Excel UI with ribbon toolbar visible
Realistic Excel 2019/365 interface, slightly messy/disorganized look"

Save output to assets/images/problem-excel.png
  </action>
  <verify>File exists at assets/images/problem-excel.png, shows realistic Excel spreadsheet</verify>
  <done>Excel spreadsheet mockup generated showing typical duty roster chaos</done>
</task>

<task type="auto">
  <name>Task 4: Generate Problem Section WhatsApp Mockup</name>
  <files>assets/images/problem-whatsapp.png</files>
  <action>
Use /nano-banana skill to generate a WhatsApp chat mockup on iPhone.

Prompt for generation:
"iPhone showing WhatsApp group chat. The chat displays:
- Group name: 'Tigers U12 Parents'
- Multiple message bubbles showing typical scheduling chaos:
  - 'I cannot make it on Saturday. Who can help?'
  - 'Sorry, working that day'
  - 'Can someone cover scoreboard? I asked John but no reply'
  - 'What time is the game again?'
- Mix of sent and received messages
- Realistic WhatsApp iOS interface with green bubbles for sent messages
- Some unread message indicators
Professional product shot, front view, showing frustration of group chat coordination"

Save output to assets/images/problem-whatsapp.png
  </action>
  <verify>File exists at assets/images/problem-whatsapp.png, shows WhatsApp chat on iPhone</verify>
  <done>WhatsApp mockup generated showing typical group chat scheduling frustration</done>
</task>

<task type="auto">
  <name>Task 5: Generate Features Section Notification Mockup</name>
  <files>assets/images/features-notification.png</files>
  <action>
Use /nano-banana skill to generate an iPhone notification mockup.

Prompt for generation:
"iPhone lock screen or home screen showing a push notification from TeamTigrr app:
- App icon: orange tiger paw or similar sports icon
- Notification title: 'Help Needed!'
- Notification body: 'Shot clock task available Saturday March 6th at 16:30. Interested?'
- Two action buttons: 'I can help' and 'Not this time'
- Clean iOS notification style
- Blurred home screen background
Professional product photography, slight angle, showing the ease of responding to duty requests"

Save output to assets/images/features-notification.png
  </action>
  <verify>File exists at assets/images/features-notification.png, shows iOS notification</verify>
  <done>Notification mockup generated showing help request feature</done>
</task>

<task type="checkpoint:human-verify" gate="blocking">
  <what-built>All 5 mockup images generated using Nano Banana Pro</what-built>
  <how-to-verify>
    1. Review each generated image in assets/images/
    2. Verify images match the intended purpose and look professional
    3. Ensure brand colors (orange #FF6B00) are present where appropriate
    4. Confirm images will work well on the landing page
  </how-to-verify>
  <resume-signal>Type "approved" to continue with HTML integration, or describe needed regenerations</resume-signal>
</task>

<task type="auto">
  <name>Task 6: Integrate Images into index.html</name>
  <files>index.html</files>
  <action>
Update index.html to use the generated images:

1. Hero Section (~line 188-250):
   - Replace the CSS-simulated "Main Card" div with an img tag for hero-laptop.png
   - Add hero-iphone.png positioned alongside (consider a device composition layout)

2. Problem Section (~line 273-341):
   - Replace the simulated Excel/WhatsApp divs with problem-excel.png and problem-whatsapp.png
   - Keep the "Before" label overlay
   - Maintain the existing rounded corners and shadow styling

3. Features Section (~line 439-466):
   - Add features-notification.png to one of the feature cards (Swaps Made Simple is ideal)
   - OR create a new visual element below the features grid

Ensure all images have:
- Proper alt text for accessibility
- loading="lazy" attribute
- Responsive sizing with max-w and w-full classes
- Maintain existing visual hierarchy and animations
  </action>
  <verify>Open index.html in browser, verify images display correctly in all sections</verify>
  <done>All mockup images integrated into landing page, replacing CSS simulations</done>
</task>

</tasks>

<verification>
- [ ] All 5 images exist in assets/images/
- [ ] Images load correctly on the page
- [ ] No broken image links
- [ ] Page layout still works on mobile and desktop
- [ ] Images are optimized (reasonable file sizes)
</verification>

<success_criteria>
- Landing page displays professional device mockups instead of CSS-simulated UI
- Hero section shows laptop + iPhone mockups
- Problem section shows Excel spreadsheet + WhatsApp chat mockups
- Features section includes notification mockup
- All images are accessible with alt text
- Page performance remains acceptable
</success_criteria>

<output>
After completion, verify the landing page visually and confirm all images display correctly.
</output>
