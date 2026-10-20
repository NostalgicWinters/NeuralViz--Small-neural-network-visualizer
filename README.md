# NeuralViz: Neural Network Computation Graph Visualizer

A neural network computation graph visualizer built on a custom, micrograd-style autograd engine. It makes backpropagation and gradient flow intuitive by showing what actually happens inside a network: **values flowing forward and gradients flowing backward.**

![NeuralViz Demo](demo.gif)

---

## Table of Contents

- [Motivation](#motivation)
- [Features](#features)
- [How It Works](#how-it-works)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
  - [Option 1: Docker (recommended)](#option-1-docker-recommended)
  - [Option 2: Run manually](#option-2-run-manually)
- [Usage](#usage)
- [Roadmap](#roadmap)
- [Credits](#credits)
- [Contributing](#contributing)

---

## Motivation

Modern deep learning frameworks hide the fundamentals of automatic differentiation behind clean APIs. NeuralViz was built to:

- Understand how autograd works under the hood
- Visualize computation graphs instead of treating them as black boxes
- Bridge the gap between the theory of backpropagation and a working implementation

It is useful for **learning, debugging, and teaching** neural networks.

## Features

- **Autograd engine from scratch**: a micrograd-style scalar value engine with reverse-mode automatic differentiation
- **Computation graph construction**: the graph is built dynamically during the forward pass
- **Backpropagation**: gradients computed via the chain rule over the graph
- **Interactive visualization** of:
  - Nodes (values and operations)
  - Edges (dependencies between nodes)
  - Forward values
  - Backward gradients
- **Automatic graph layout** for readable diagrams, even as the network grows

## How It Works

1. **Forward pass:** each operation (`+`, `*`, activation, etc.) creates a new node that remembers its inputs, so a directed acyclic graph is built as the computation runs.
2. **Backward pass:** starting from the output, the engine walks the graph in reverse topological order, applying the chain rule at each node to accumulate gradients.
3. **Visualization:** the backend exposes the graph (nodes, edges, values, gradients), and the frontend renders and lays it out so you can inspect every step.

## Tech Stack

| Layer | Technology |
| --- | --- |
| Autograd engine | Custom micrograd-style implementation (from scratch) |
| Backend | Served on port `8000` (Dockerized) |
| Frontend | [React Flow](https://reactflow.dev/) + [elkjs](https://github.com/kieler/elkjs), served by Vite on port `5173` |
| Orchestration | Docker Compose |

## Project Structure

```
.
├── backend/              # Autograd engine + API serving the computation graph
├── frontend/             # React app: graph rendering and layout
├── docker-compose.yml    # Runs backend and frontend together
├── demo.gif              # Demo of the visualizer
├── package.json
└── README.md
```

## Getting Started

### Prerequisites

- [Docker](https://www.docker.com/) and Docker Compose (for Option 1), **or**
- [Node.js](https://nodejs.org/) 22+ and a recent Python 3 installation (for Option 2)

### Option 1: Docker (recommended)

```bash
git clone https://github.com/NostalgicWinters/NeuralViz--Small-neural-network-visualizer.git
cd NeuralViz--Small-neural-network-visualizer

docker compose up --build
```

Then open:

- **Frontend:** http://localhost:5173
- **Backend:** http://localhost:8000

### Option 2: Run manually

**Backend**

```bash
cd backend
# install the dependencies listed in the backend folder, then start the server on port 8000
```

**Frontend**

```bash
cd frontend
npm install
npm run dev
```

Open http://localhost:5173 in your browser.

> Make sure the backend is running on port `8000` before using the frontend.

## Usage

1. Start the app (see above) and open the frontend in your browser.
2. Run a forward pass to see the computation graph with each node's value.
3. Run backpropagation to see gradients appear on every node.
4. Pan, zoom, and inspect individual nodes to follow how values and gradients move through the network.

## Roadmap

Ideas for future improvements:

- [ ] Support for larger networks and custom architectures
- [ ] Step-by-step backprop animation
- [ ] Training loop visualization (loss curve, weight updates)
- [ ] Export graph as an image

## Credits

This project is heavily inspired by [Andrej Karpathy](https://karpathy.ai/)'s educational work on neural networks and automatic differentiation, particularly his [micrograd](https://github.com/karpathy/micrograd) walkthroughs.

- The autograd engine follows the micrograd philosophy
- All code was written independently for learning purposes
- The visualization and extensions are original additions

If you haven't already, his work is highly recommended.

## Contributing

Contributions, issues, and feature requests are welcome. Feel free to open an issue or submit a pull request.

If you find this project helpful:

- ⭐ Star the repository
- 🍴 Fork it
- Share feedback or open an issue
