# RIX: Robot Interprocess eXchange

**A lightweight, modular framework for building educational robotics applications**

RIX (Robot Interprocess eXchange) is a modern robot operating system designed specifically for education. It provides fast, reliable interprocess communication with minimal dependencies, making it perfect for learning robotics concepts and building real-world robotic systems.

---

## 🌟 Why RIX?

- **🎓 Education-Focused**: Simple, clean APIs designed for learning and teaching robotics
- **🚀 Fast & Lightweight**: Zero third-party dependencies in core libraries, optimized for performance
- **🧩 Modular Architecture**: Publishers, subscribers, services, actions, and timers
- **🌐 Multi-Language**: Full support for C++ and Python with consistent APIs
- **🤖 Robotics-Ready**: Built-in support for transforms, kinematics, and robot models
- **🔒 Reliable**: TCP-based communication ensures message integrity

---

## 📦 Repositories

### [rix-cpp](https://github.com/rix-ros/rix-cpp)
The core C++ implementation of RIX, providing high-performance interprocess communication.

**Features:**
- Publishers, subscribers, services, and action servers/clients
- Transform trees (`rix::tf`) for 3D spatial transforms
- Robot model parsing and kinematics (`rix::rob`)
- Timer callbacks and parameter servers
- Unit testing support with GTest

### [rix-py](https://github.com/rix-ros/rix-py)
Python bindings and tools for RIX, making robotics programming accessible in Python.

**Features:**
- Full Python API matching the C++ interface
- Transform broadcasting and listening
- Robot model visualization with Open3D
- Command-line tools: `rixinfo` for system introspection
- Video streaming support with OpenCV

### [rix-msg](https://github.com/rix-ros/rix-msg)
Cross-language message definition and serialization library.

**Features:**
- Define messages once, generate code for C++ and Python
- Zero-copy serialization for low-latency communication
- Type-safe schema validation
- Human-readable JSON message definitions
- CLI tool: `rixmsg` for managing message packages

### [jrdf](https://github.com/rix-ros/jrdf)
JSON Robot Description Format - a modern alternative to URDF.

**Features:**
- Convert URDF to JRDF format
- Validate robot models with JSON schema
- 3D visualization with Open3D
- Support for meshes, textures, and materials
- Macro system for parameterized models

---

## 🚀 Quick Start

### Installation

Requires Python 3.12 and CMake 3.16+. Install on POSIX-compliant systems (Linux, macOS):

```bash
git clone https://github.com/rix-ros/rix-cpp.git
cd rix-cpp
bash install.bash
```

This installs all RIX components to `~/.rix/`.

### Environment Setup

Source the setup script before using RIX:

```bash
source ~/.rix/setup.bash
```

Add to your shell profile for convenience:

```bash
echo 'source ~/.rix/setup.bash' >> ~/.bashrc
```

### Start RIXHub

The central discovery service for RIX nodes:

```bash
rixhub
```

---

## 💡 Usage Examples

### C++ Publisher

```cpp
#include "rix/rix.hpp"
#include "rix/std_msgs/Header.hpp"

using namespace rix;

int main() {
  Node node("publisher_node");
  auto pub = node.create_publisher<std_msgs::Header>("/my_topic");
  
  node.create_timer(Duration(1.0), [&](auto) {
    std_msgs::Header msg;
    msg.frame_id = "Hello, RIX!";
    pub->publish(msg);
  });
  
  node.spin();
}
```

### Python Subscriber

```python
from rix.core import Node
from rix.std_msgs import Header

def callback(msg: Header):
    print(f"Received: {msg.frame_id}")

node = Node("subscriber_node")
node.create_subscriber(Header, "/my_topic", callback)
node.spin()
```

---

## 🛠️ Command-Line Tools

RIX includes several CLI tools for development and debugging:

- **`rixhub`** - Central discovery and mediation service
- **`rixmsg`** - Manage and generate message definitions
- **`rixinfo`** - Introspect running nodes, topics, and services
- **`jrdf`** - Create, validate, and visualize robot models

### Examples

```bash
# List all active nodes
rixinfo node list

# Echo messages on a topic
rixinfo topic echo /my_topic

# Display runtime graph
rixinfo graph

# Create message implementations
rixmsg create defs/my_msgs/

# Visualize a robot model
jrdf visualize my_robot
```

---

## 📚 Learn More

- [RIX C++ Documentation](https://github.com/rix-ros/rix-cpp)
- [RIX Python Documentation](https://github.com/rix-ros/rix-py)
- [Message Library Documentation](https://github.com/rix-ros/rix-msg)
- [JRDF Documentation](https://github.com/rix-ros/jrdf)

---

## 🎯 Use Cases

RIX is perfect for:

- **Robotics Education**: Teaching fundamental concepts in robot software architecture
- **Research Prototyping**: Rapidly developing and testing robotic algorithms
- **Multi-Robot Systems**: Building distributed robotic applications
- **Real-Time Control**: Low-latency communication for control loops
- **Simulation Integration**: Connecting simulators with real hardware

---

## 🤝 Contributing

We welcome contributions! Please see individual repository README files for contribution guidelines.

---

## 📄 License

RIX is released under the BSD 3-Clause License. See [LICENSE.md](LICENSE.md) for details.

**Copyright (c) 2025, Broderick Riopelle, Odest Chadwicke Jenkins**

---

## 🙏 Acknowledgments

RIX is developed for educational purposes, making robotics programming accessible to students and researchers worldwide.

---
