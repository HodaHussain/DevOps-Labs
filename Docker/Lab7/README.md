# Lab 7: Multi-Network Microservices, Volumes, and Bind Mounts

## Objective
Deploy a multi-service application using Docker, custom bridge networks, Docker volumes, and bind mounts.

## Application Architecture
The application consists of three services:

- **Frontend:** Flask web application running on port `3000`.
- **Backend:** Flask API running on port `5000`, responsible for creating and retrieving messages.
- **Notification:** Flask service running on port `5001`, responsible for receiving notifications.

## Docker Images
Built the three Docker images successfully:

- `lab7-frontend`
- `lab7-backend`
- `lab7-notification`

## Docker Networks
Created two custom bridge networks with separate subnets:

| Network | Subnet | Connected Services |
|---|---|---|
| `lab7-frontend-backend` | `172.28.0.0/16` | Frontend, Backend |
| `lab7-backend-notification` | `172.29.0.0/16` | Backend, Notification |

The Backend is connected to both networks to enable communication between the services.

## Volumes and Bind Mounts

Created two Docker volumes:

- `lab7-backend-logs` mounted at `/app/logs` in the Backend container.
- `lab7-notification-logs` mounted at `/app/logs` in the Notification container.

Created a host directory named `backend-data` and mounted it at `/app/data` in the Backend container to persist application data.

## Container Configuration

- **Notification:** Connected to `lab7-backend-notification`.
- **Backend:** Connected to both networks, configured with the Notification URL, and provided with its log volume and data bind mount.
- **Frontend:** Connected to `lab7-frontend-backend`, configured with the Backend URL, and published for browser access.

## Testing and Verification

- Confirmed that all three application containers were running.
- Opened the Frontend web page successfully.
- Created a message: `Hello from Lab 7`.
- Verified that the message appeared in the Messages section.
- Confirmed that the message was saved in `backend-data/messages.json`.
- Verified that the Notification service received the message and returned HTTP `200`.

## Port Note

Port `8080` was already occupied by Jenkins on the VM. Therefore, the Frontend was tested successfully using host port `18080`, mapped to container port `3000`.

The application was accessible at `http://localhost:18080` from the VM.

## Screenshots

Screenshots demonstrating image builds, network and volume creation, running containers, Frontend testing, persistent data, and Notification logs will be added to this folder.
<img width="1156" height="796" alt="Screenshot 2026-10-24 013438" src="https://github.com/user-attachments/assets/4f75f719-b167-4544-9055-16d4a1082b44" />
<img width="1198" height="747" alt="Screenshot 2026-10-24 013216" src="https://github.com/user-attachments/assets/0ac72781-94dd-4318-94d6-2c7cf9935aac" />
<img width="1035" height="341" alt="Screenshot 2026-10-24 012835" src="https://github.com/user-attachments/assets/19e2f168-7cc7-4da7-9e89-77abeee7fc4d" />
<img width="1177" height="660" alt="Screenshot 2026-10-24 105017" src="https://github.com/user-attachments/assets/c0290705-3616-45f6-90ca-306d3341941d" />
<img width="1187" height="250" alt="Screenshot 2026-10-24 104518" src="https://github.com/user-attachments/assets/ead5ca1e-d4e8-40a2-aee6-d0c2170a3e3b" />
<img width="1215" height="926" alt="Screenshot 2026-10-24 014956" src="https://github.com/user-attachments/assets/92282ff2-2a83-4c65-a09d-f76d16b42ddd" />
<img width="1250" height="810" alt="Screenshot 2026-10-24 013619" src="https://github.com/user-attachments/assets/544a6555-a22a-4770-881a-eecf17110551" />
