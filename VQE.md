## Variational Quantum Eigensolver
Surgió en el año 2013
perfecto en la generación NISQ
Alberto Peruzzo, McClean, Shadbolt, et al. 

---
## Chatsito
 El algoritmo de Variational Quantum Eigensolver (VQE) es uno de los algoritmos más populares para aplicaciones de química cuántica en las computadoras cuánticas actuales. Aquí te dejo un ejemplo de código en PennyLane para implementar el VQE:

```python
import pennylane as qml
from pennylane import numpy as np

# Define la función de circuito cuántico
def ansatz(params, wires):
    qml.RX(params[0], wires=0)
    qml.RY(params[1], wires=0)
    qml.CNOT(wires=[0, 1])
    qml.RZ(params[2], wires=1)
    qml.CNOT(wires=[0, 1])
    qml.RX(params[3], wires=0)
    qml.RY(params[4], wires=0)

# Define la función de costo
def cost(params):
    ans = ansatz(params, wires)
    return qml.expval(qml.PauliZ(0) @ qml.PauliZ(1))

# Define los parámetros y los dispositivos 
params = np.random.randn(5)
dev = qml.device("default.qubit", wires=2)

# Define y optimiza el circuito cuántico
@qml.qnode(dev)
def circuit(params):
    ansatz(params, wires)
    return qml.expval(qml.PauliZ(0) @ qml.PauliZ(1))

opt = qml.GradientDescentOptimizer(stepsize=0.4)
steps = 100
for i in range(steps):
    params = opt.step(cost, params)

# Ejecuta el circuito optimizado
energy = circuit(params)
print("Energía: ", energy)
```

Recuerda que este es solo un ejemplo básico y que la implementación del VQE depende completamente del problema específico que estés tratando de resolver.
