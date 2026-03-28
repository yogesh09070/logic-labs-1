# ⚡ LogicLab – Interactive Logic Gate Simulator

A cloud-ready SaaS digital logic circuit simulator with drag-and-drop building, real-time simulation, truth table generation, and 30+ prebuilt circuit templates.

🌐 **Live Demo**: [logiclab-kappa.vercel.app](https://logiclab-kappa.vercel.app)

---

## ✨ Features

- **Drag-and-Drop Builder** – Place gates (AND, OR, NOT, NAND, NOR, XOR, XNOR) with 2, 3, or 4 inputs
- **Real-Time Simulation** – Toggle inputs and watch signals propagate with animated color-coded wires (🟢 HIGH / 🔴 LOW)
- **Truth Table Generator** – Auto-generates full truth tables with active row highlighting and CSV export
- **30+ Prebuilt Templates** – Across 6 categories:
  - **Basic**: AND, OR, NOT gates
  - **Combinational**: Half/Full Adder, Subtractor, MUX, DEMUX, Decoder, Encoder
  - **Sequential**: SR Latch, D/JK/T Flip-Flops, Shift Register, Counter
  - **Arithmetic**: 4-Bit Ripple Carry Adder, 4-Bit Magnitude Comparator
  - **Data Routing**: 4:1 MUX (3-in AND), 1:4 DEMUX, 3-to-8 Decoder, 4-to-16 Decoder
  - **Error Detection**: Parity Generator/Checker, Binary-to-Gray Converter, BCD to 7-Segment
- **Undo/Redo** – Full history with Ctrl+Z / Ctrl+Y
- **Delete Components** – Select and delete nodes/wires
- **Save & Load** – Local storage with cloud-ready Supabase integration
- **Beginner Mode** – Tooltips explaining every gate
- **Dark Neon Theme** – Futuristic UI with glow effects and smooth animations

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 18 + Vite 5 |
| Styling | TailwindCSS 3 |
| Circuit Canvas | React Flow (@xyflow/react) |
| State Management | Zustand |
| Auth & Database | Supabase (ready) |
| Deployment | Vercel |

---

## 🚀 Quick Start

```bash
# Install dependencies
npm install

# Start dev server
npm run dev

# Build for production
npm run build
```

---

## 📁 Project Structure

```
src/
├── components/       # Navbar, Sidebar, TruthTablePanel
├── gates/            # Custom React Flow nodes
│   ├── GateNode.jsx       # Logic gate (AND, OR, etc.)
│   ├── InputNode.jsx      # Toggle switch input
│   ├── OutputNode.jsx     # Output display
│   └── CustomEdge.jsx     # Animated signal wire
├── pages/            # Route pages
│   ├── LandingPage.jsx    # Hero landing page
│   ├── BuilderPage.jsx    # Main circuit builder
│   ├── DashboardPage.jsx  # Saved circuits
│   ├── LoginPage.jsx      # Auth page
│   └── SharedViewPage.jsx # Public circuit viewer
├── simulator/        # Logic engine
│   ├── gates.js           # Gate functions & metadata
│   └── engine.js          # Topological sort evaluator
├── store/            # Zustand state management
│   └── circuitStore.js    # Central store with undo/redo
├── templates/        # 30+ prebuilt circuit definitions
├── truthTable/       # Truth table generator + CSV export
└── utils/            # Supabase client config
```

---

## 🎮 How to Use

1. Open the **Builder** page
2. Add **Input** and **Output** nodes from the sidebar
3. Drag **logic gates** (2-in, 3-in, or 4-in) onto the canvas
4. **Connect** nodes by dragging from output handles to input handles
5. **Click inputs** to toggle between 0 and 1
6. Watch signals propagate in real-time
7. Open the **Truth Table** panel to see all combinations
8. Use **Undo/Redo** (Ctrl+Z/Y) and **Delete** (Del key) as needed

---

## ⌨️ Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+Z` | Undo |
| `Ctrl+Y` | Redo |
| `Delete` | Delete selected |
| `Ctrl+S` | Save circuit |

---

## 🔗 Deployment

### Vercel
```bash
npm install -g vercel
vercel
```

### Supabase Setup (for cloud features)

1. Create a project at [supabase.com](https://supabase.com)
2. Run this SQL in the SQL Editor:
```sql
CREATE TABLE circuits (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  user_id UUID REFERENCES auth.users(id) ON DELETE CASCADE,
  name TEXT NOT NULL DEFAULT 'Untitled Circuit',
  nodes JSONB NOT NULL DEFAULT '[]',
  edges JSONB NOT NULL DEFAULT '[]',
  is_public BOOLEAN DEFAULT false,
  created_at TIMESTAMPTZ DEFAULT NOW(),
  updated_at TIMESTAMPTZ DEFAULT NOW()
);
ALTER TABLE circuits ENABLE ROW LEVEL SECURITY;
```
3. Copy `.env.example` → `.env` and fill in your Supabase credentials

---

## 📄 License

MIT

---

**Built with ❤️ using React, Vite, and React Flow**
