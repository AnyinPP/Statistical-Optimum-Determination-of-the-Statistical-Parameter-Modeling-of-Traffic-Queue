# Statistical-Optimum-Determination-of-the-Statistical-Parameter-Modeling-of-Traffic-Queue
Statistical Optimum Determination of the Statistical Parameter Modeling of Traffic Queue

import numpy as np
import matplotlib.pyplot as plt

# Parameters for simulation
true_arrival_rate = 0.5  # vehicles per second
true_service_rate = 0.3  # services per second
simulation_duration = 1000  # seconds
recording_interval = 1  # second

# Simulate the queueing process
np.random.seed(42)  # For reproducibility
time_points = np.arange(0, simulation_duration, recording_interval)
queue_lengths = []
current_queue_length = 0
arrivals_list = []
services_list = []

for t in time_points:
    arrivals = np.random.poisson(true_arrival_rate * recording_interval)
    services = np.random.poisson(true_service_rate * recording_interval)
    current_queue_length = max(0, current_queue_length + arrivals - services)
    queue_lengths.append(current_queue_length)
    arrivals_list.append(arrivals)
    services_list.append(services)

# Plotting the true queue lengths
plt.figure(figsize=(12, 6))
plt.plot(time_points, queue_lengths, label='True Queue Length')
plt.xlabel('Time (seconds)')
plt.ylabel('Queue Length')
plt.title('Simulated Traffic Queue Length Over Time')
plt.legend()
plt.grid(True)
plt.show()
