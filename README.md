# Demo Skins and Dialogs Module

This folder contains a Morweb demo module that showcases administrative UI prototypes (index tables, dialogs, and navigation widgets) for designers. The code is organized as a set of PHP controllers and view templates plus supporting JavaScript and CSS assets.

## Layout and responsibilities
- **`section.php`** defines `mwDemoInit`, which registers the demo module (`demo` namespace), its display name, and descriptive metadata used by the hosting Morweb instance.
- **`backend/Skins.php`** exposes the `Skins` controller. The `index` action validates the subsection parameter, loads demo content (such as the desktop and index fragments), and queues UI resources like TinyMCE, date pickers, and drag-and-drop helpers before rendering.
- **`views/desktop.php`** builds the main desktop view by loading the sample dialog window (`wDialog`) and enqueueing demo scripts/styles. It injects the rendered index fragment into the desktop shell.
- **`views/index.php`** contains the nested “Index Table” markup that demonstrates sortable, nestable list rows and dynamic cells. The accompanying script walks the `.dyna` elements and fills them using `myUpdateDyna` from `res/js/sample.js`.
- **`views/dialogs/`** holds individual dialog templates used by the desktop. For example, `wCombo.php` assembles multiple dialog and form fragments into a tabbed window, loading shared skin styles via helper calls.
- **`widgets/system/NavGroup_Demo.php`** adds a navigation group to expose the demo entry points (Skins and Dialogs) in the admin UI.
- **`res/js/sample.js`** defines `myUpdateDyna`, a tiny helper that replaces placeholder values in dynamic cells.
- **`res/css/sample.css`** tweaks visual treatment for specific table cells in the demo index.

## How it fits together
1. Morweb loads `mwDemoInit` from `section.php` to register the demo module.
2. Requests routed to the module hit `backend/Skins.php`. The controller composes a data array, loads the index content, and adds required frontend resources.
3. `views/desktop.php` renders the desktop chrome and injects the rendered index markup from `views/index.php`.
4. The browser initializes `res/js/sample.js` to populate dynamic cells and apply styling from `res/css/sample.css`.
5. Optional dialogs from `views/dialogs/` can be displayed (e.g., via the “Dialog” button) to showcase stacked or tabbed window layouts.

## Next steps
- Replace placeholder copy and demo markup with production-ready content and real data sources.
- Flesh out controller logic to read/write actual records instead of static fixtures.
- Standardize dialog templates, removing unused prototypes and documenting expected parameters.
- Add automated tests or snapshot coverage to detect regressions in the UI scaffolding.
- Document the resource pipeline (JS/CSS loading) for future contributors and integrate with the broader Morweb build process.
