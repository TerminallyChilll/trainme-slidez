# TrainMe Slidez - Mobile-First Training Presentation System

TrainMe Slidez is a static HTML slideshow application designed for training presentations. It provides a presenter control interface and an audience viewer interface with real-time synchronization via Supabase. The application is optimized for mobile devices and works entirely with static file serving.

Always reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.

## Working Effectively

### Bootstrap and Run the Application
- No build process required - this is a static HTML application
- No dependencies to install - uses CDN imports for all external resources
- Serve the application using any static file server:
  - `python3 -m http.server 8000` - serves on http://localhost:8000 (starts in 1-2 seconds)
  - Alternative: `python -m SimpleHTTPServer 8000` (Python 2, if available)
  - Alternative: `npx serve .` (if Node.js is available)
  - Alternative: Use VS Code Live Server extension
- NEVER CANCEL the server - let it run in the background during development
- CRITICAL: Always use HTTP server - opening files directly (file://) will fail due to CORS restrictions

### Running and Testing the Application
- Start server: `python3 -m http.server 8000` - takes 1-2 seconds to start
- Open presenter interface: `http://localhost:8000/presenter.html`
- Open viewer interface: `http://localhost:8000/viewer.html`
- View individual slides: `http://localhost:8000/page_1.html` through `http://localhost:8000/page_18.html`
- Test mobile responsiveness using browser developer tools device emulation

### Key Application Files
- `presenter.html` - Presenter control interface for managing slides and sessions
- `viewer.html` - Audience viewer interface that follows presenter automatically
- `page_1.html` through `page_18.html` - Individual slide content pages
- `mobile.css` - Mobile-responsive CSS styles for optimal viewing on all devices
- `.gitattributes` - Git configuration for line endings

## Validation

### Complete User Scenarios - ALWAYS Test These After Changes
1. **Presenter Workflow:**
   - Open `presenter.html` in browser
   - Enter a session code (e.g., "1234")
   - Click "Start session" 
   - Use "Next ▶︎" and "◀︎ Prev" buttons to navigate slides
   - Verify slide preview shows in iframe
   - Test keyboard shortcuts (left/right arrow keys)

2. **Viewer Workflow:**
   - Open `viewer.html?code=1234` in another browser tab/window
   - Verify it automatically joins the session
   - Confirm slides sync when presenter changes slides
   - Test manual join by entering code on join screen

3. **Individual Slide Testing:**
   - Open each `page_*.html` file directly
   - Verify content displays correctly
   - Test mobile responsiveness by resizing browser
   - Confirm images and styling load properly

4. **Mobile Responsiveness:**
   - Test all interfaces on mobile viewport sizes
   - Verify touch interactions work correctly
   - Confirm readable text and proper scaling

### Critical Limitations to Document
- **Internet Connection Required:** Supabase and CDN resources require internet access for full functionality
- **Cross-Origin Restrictions:** Files must be served via HTTP server - opening HTML files directly (file://) will fail due to CORS and ES module restrictions
- **Browser Compatibility:** Modern browsers required for ES module support (Chrome 61+, Firefox 60+, Safari 11+)
- **Supabase Dependency:** Real-time sync requires Supabase service to be available and accessible
- **CDN Dependencies:** External CDN resources (TailwindCSS, FontAwesome) may be blocked in restricted environments

## Application Architecture

### Technology Stack
- **Frontend:** Pure HTML5, CSS3, ES6 modules
- **Styling:** TailwindCSS (CDN), Font Awesome (CDN), custom mobile.css
- **Real-time Sync:** Supabase broadcast channels
- **No Build Tools:** Direct browser execution of ES modules
- **No Backend:** Completely client-side application

### File Structure
```
.
├── .github/
│   └── copilot-instructions.md
├── .git/
├── .gitattributes
├── mobile.css                 # Mobile-responsive styles
├── presenter.html             # Presenter control interface
├── viewer.html               # Audience viewer interface
├── page_1.html               # Slide 1: Title slide
├── page_2.html               # Slide 2: Overview
├── ...                       # Additional slides
└── page_18.html              # Slide 18: Final slide
```

### External Dependencies (CDN)
- `@supabase/supabase-js@2` - Real-time synchronization
- `tailwindcss` - CSS framework
- `font-awesome` - Icon fonts
- All dependencies are loaded via CDN - no local installation needed

## Common Development Tasks

### Adding New Slides
1. Create new HTML file following naming pattern: `page_19.html`, `page_20.html`, etc.
2. Update the slides array in both `presenter.html` and `viewer.html`:
   ```javascript
   const slides = [
     "page_1.html",
     "page_2.html",
     // ... existing slides
     "page_19.html",  // Add new slide here
     "page_20.html"   // Add new slide here
   ];
   ```
3. Test navigation works correctly
4. Verify mobile responsiveness

### Modifying Slide Content
1. Edit the target `page_*.html` file directly
2. Follow existing slide structure and styling patterns
3. Maintain mobile.css responsive design principles
4. Test changes by serving locally and viewing the specific slide

### Customizing Appearance
1. Edit `mobile.css` for global styling changes
2. Modify individual slide HTML for slide-specific changes
3. Update Tailwind classes in slide content as needed
4. Always test mobile responsiveness after styling changes

### Troubleshooting Common Issues
1. **Slides not loading:** Verify HTTP server is running and files are accessible
2. **Sync not working:** Check browser console for Supabase connection errors
3. **Styling issues:** Verify CDN resources are loading (check Network tab)
4. **Mobile display problems:** Test with browser dev tools device emulation

## No Build, Test, or Lint Process
- **No package.json:** This is a pure HTML/CSS/JS application
- **No build step:** Files are served directly to browser
- **No tests:** Manual testing via browser is the validation method
- **No linting:** Use browser console and validation tools as needed
- **No CI/CD:** Repository contains ready-to-serve static files

## Development Workflow
1. Make changes to HTML, CSS, or update slide content
2. Refresh browser to see changes immediately
3. Test complete user scenarios for any UI/UX changes
4. Verify mobile responsiveness for any styling changes
5. Test cross-browser compatibility for JavaScript changes

Always serve the application via HTTP server during development - do not open HTML files directly in browser as this may cause CORS and module loading issues.