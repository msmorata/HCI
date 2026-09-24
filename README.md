# Apex WMS — Warehouse Inventory & Order Management System
## Interactive Prototype for Human-Computer Interaction (HCI) Midterm

An interactive, high-fidelity web prototype demonstrating the **Industrial Precision (Neo-Logistics)** design style and the **Separation of Concerns (SoC)** software architecture, engineered specifically to satisfy the HCI Midterm project criteria and defend **Shneiderman's Eight Golden Rules of Interface Design**.

---

## 🏛️ Architecture: Strict Separation of Concerns (SoC)

The application cleanly decouples markup structure, visual presentation, and interactive behavior into dedicated layers:

```
bold-oppenheimer/
├── index.html                  # 1. STRUCTURE: Pure semantic HTML5 markup (zero inline CSS, zero inline JS)
├── css/                        # 2. PRESENTATION: Modular CSS with Design Tokens
│   ├── phosphor/               # Standardized Icon Library: Phosphor web font & styles (100% offline)
│   ├── tokens.css              # Industrial Precision design tokens (surfaces, colors, typography, elevations)
│   ├── base.css                # CSS reset, accessible focus visible states, and font styling
│   ├── layout.css              # App shell, responsive deep-slate sidebar, header, and grid systems
│   └── components.css          # UI components: data tables, status badges, modals, toasts, steppers
└── js/                         # 3. BEHAVIOR & STATE: Modular JavaScript
    ├── data.js                 # Data layer: seed inventory, orders, deliveries, audit movements, and user
    ├── store.js                # State layer: central reactive state store, localStorage persistence, undo stack
    ├── ui.js                   # Presentation helpers: toast alerts with undo callbacks, modal controller
    ├── router.js               # Navigation layer: module view switching and breadcrumb controller
    └── app.js                  # Application coordinator: event orchestration and user flows
```

---

## 🚀 How to Run the Prototype

No compilation, bundler, or `npm install` is required! The prototype works out-of-the-box in any modern browser:

### Option A: Direct Open
Simply double-click [`index.html`](file:///Users/dave-ojt/Documents/antigravity/bold-oppenheimer/index.html) or open it directly in Chrome, Safari, Firefox, or Edge.

### Option B: Local Static Server (Recommended)
You can also launch a lightweight local server:
```bash
# Python 3
python3 -m http.server 8080

# Or via Node.js
npx serve .
```
Then visit `http://localhost:8080` in your browser.

---

## 📦 Seven Required Modules Implemented

| Module | Purpose & Features | Screen Identifier |
| :--- | :--- | :--- |
| **Module 1: Login & User Management** | User authentication with email/password, error feedback, terminal remember checkbox, demo auto-fill, and session logout. | `#view-login` |
| **Module 2: Warehouse Dashboard** | Operational overview with KPI cards (Total Products, Available Stock, Low Stock, Pending Orders), quick workflow links, and recent activity log. | `#module-dashboard` |
| **Module 3: Inventory Management** | Comprehensive product catalog with instant search, category filtering, stock status filtering, Add/Edit product modals, details inspection, and delete confirmation. | `#module-inventory` |
| **Module 4: Receiving Management** | Inbound shipment verification log and multi-step delivery wizard (`Manifest → Inspection → Confirmation`) that automatically increments stock levels and records movements. | `#module-receiving` |
| **Module 5: Order & Picking** | Customer order queue with lifecycle statuses (`Pending → Picking → Ready → Completed`), item-by-item barcode/location checklist, and real-time picking progress bar. | `#module-orders` |
| **Module 6: Stock Tracking** | Immutable audit trail displaying all warehouse movements (`Received`, `Released`, `Transferred`, `Adjusted`), before/after stock transitions, and responsible personnel. | `#module-movements` |
| **Module 7: Reports & Alerts** | Low-stock replenishment report with one-click reorder shortcuts and system notification center with unread status indicators. | `#module-reports` |

---

## 🔄 The Three Required User Flows

### User Flow 1 — Receive New Inventory
$$\text{Login} \rightarrow \text{Dashboard} \rightarrow \text{Receiving} \rightarrow \text{Enter Information} \rightarrow \text{Review} \rightarrow \text{Confirm}$$
1. On the Login screen, click **"Auto-fill Demo"** and **"Sign In to Terminal"**.
2. Click **"Receive Delivery"** in the top header (or navigate to **Receiving** in the sidebar).
3. Fill out the Delivery Number (e.g. `DEL-9901-X`), choose a product line, quantity (e.g. `30`), and condition.
4. Click **"Review Inbound →"** to inspect the manifest summary.
5. Click **"Confirm & Update Stock"**. Notice the instant success toast, the stock increase in Module 3, and the automatic audit log created in Module 6.

### User Flow 2 — Process an Order
$$\text{Dashboard} \rightarrow \text{Orders} \rightarrow \text{Select Order} \rightarrow \text{Picking} \rightarrow \text{Update Status} \rightarrow \text{Complete}$$
1. On the Dashboard or Sidebar, navigate to **Order & Picking**.
2. On order `ORD-9402`, click **"Continue Picking"**.
3. Check off the remaining items. Observe the live progress bar advancing from `33%` to `100%` and status updating to **Ready**.
4. Click **"Complete Order & Dispatch"** to finalize fulfillment. Notice stock deduction and audit log generation.

### User Flow 3 — Manage Low Stock
$$\text{Dashboard} \rightarrow \text{Low Stock} \rightarrow \text{Inventory} \rightarrow \text{Product Details} \rightarrow \text{Review}$$
1. From the **Dashboard**, click directly on the **"Low / Critical Stock"** KPI card.
2. The view automatically transitions to **Inventory Management** pre-filtered to show only **Low Stock** items.
3. Click **"View"** on any low stock item (e.g. `SKU-SAF-441`) to open the **Product Specification & Stock Info** modal to review threshold, location, and supplier.

---

## 🏆 Midterm Presentation Defense: Shneiderman's Eight Golden Rules

When presenting to your instructor, use the built-in **"HCI Rules Guide"** button in the bottom-left of the prototype or reference these points:

1. **Strive for Consistency:**  
   Standardized 3-tier master layout (Deep Slate `#0F172A` sidebar, sticky top header, white bordered cards), consistent button semantics, and unified typography across all 7 modules.
2. **Seek Universal Usability:**  
   High contrast (WCAG AAA compliant text against white/slate canvas), distinct click targets (minimum 40px), and keyboard shortcuts (press `/` anywhere to focus search, `Esc` to close any modal).
3. **Offer Informative Feedback:**  
   Color-coded status badges with dot indicators (`● In Stock`, `● Picking`), dynamic progress meters, and floating toast notifications for every user action.
4. **Design Dialogs to Yield Closure:**  
   Step-by-step progress stepper on Inbound Receiving (`1. Manifest → 2. Review → 3. Confirmation`) providing a clear sequence with definitive closure upon completion.
5. **Prevent Errors:**  
   Disabled submit button in picking run until 100% of items are checked; numeric constraint guards (`min="0"`); explicit double-confirmation modal before deleting products.
6. **Permit Easy Reversal of Actions (Undo):**  
   Floating toast alert features an interactive **`[Undo]`** button (and supports <kbd>Ctrl+Z</kbd>) when completing orders, receiving shipments, or deleting catalog products.
7. **Keep Users in Control:**  
   Cancel and back buttons on every dialog; sticky navigation sidebar allowing instant jumps between modules; dynamic search and filtering chips.
8. **Reduce Short-Term Memory Load:**  
   Monospace location tags (e.g. `Z-A1-S02`) and SKU badges remain visible in the picking checklist and receiving reviews so operators never need to memorize shelf coordinates.
