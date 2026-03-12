# MindStack Backend (Student Project)

This is the server-side repository for **MindStack**, a quiz-based learning platform. Developed as a final-year university assignment, this project is currently an **incomplete work-in-progress** and is intended strictly for **educational and non-commercial purposes**.

## 📌 Project Overview

The MindStack Backend provides a set of REST APIs and WebSocket services to support quiz management and user progress tracking. As a student learning project, it focuses on building a scalable architecture using the NestJS framework.

### Main Features (WIP)
* **Authentication**: Basic user management and secure access control integrated with Firebase.
* **Quiz Engine**: Core logic for managing quizzes, questions, and processing student test attempts.
* **Real-time Updates**: Experimental WebSocket implementation for broadcasting notifications and live leaderboard updates.
* **Payment Integration**: A simple, experimental integration with ZaloPay to explore premium subscription flows.
* **Data Management**: Structured data handling using MongoDB and Mongoose for flexible quiz schemas.

## 🛠 Tech Stack

This project served as a foundation for exploring modern backend development patterns:
* **Framework**: [NestJS](https://nestjs.com/) (Node.js framework) for a modular and maintainable architecture.
* **Language**: TypeScript for type-safe server-side logic.
* **Database**: MongoDB with Mongoose for document-based data storage.
* **Security**: Firebase Admin SDK for identity verification.
* **Communication**: Socket.io for basic real-time bi-directional communication.
* **Documentation**: Basic Swagger/OpenAPI integration for API exploration.

## 📂 Basic Structure

* `src/quizzes`: Modules for quiz and question management logic.
* `src/test-attempts`: Handles the logic for student submissions and score calculations.
* `src/notifications`: WebSocket gateways for real-time notification delivery.
* `src/payments`: Experimental service for ZaloPay transaction handling.
* `src/auth`: Security guards and Firebase strategy implementation.

## 🚀 How to Run (Local Development)

*Note: You will need a MongoDB instance and Firebase credentials to run this project fully.*

1.  **Clone the project**:
    ```bash
    git clone [https://github.com/your-username/mindstack-backend.git](https://github.com/your-username/mindstack-backend.git)
    ```
2.  **Install dependencies**:
    ```bash
    npm install
    ```
3.  **Environment Setup**:
    Create a `.env` file based on `.env.example` and provide your database URI and Firebase configuration.
4.  **Run in development mode**:
    ```bash
    npm run start:dev
    ```
## 🐳 Docker Support (Optional)

As part of my learning process with containerization, I have included a basic Docker configuration to simplify environment setup. This allows the backend and database to run in isolated containers.

### Quick Start with Docker Compose
If you have Docker installed, you can start the system without manual configuration:

1. **Build and start services**:
   ```bash
   docker-compose up --build
2. Access the API: The server will be available at http://localhost:3000.

Note: This is an experimental setup and is primarily used to ensure consistent behavior across different development environments.
## ⚠️ Disclaimer

This project is a **student assignment**. It is provided "as-is" with many features still in an experimental or unoptimized state. It is not intended for production environments or commercial use. All third-party services (like ZaloPay or Firebase) are integrated purely for learning purposes.
