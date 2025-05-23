# CampusCanteen - Food Ordering System

## Overview

CampusCanteen is a web application that allows users to browse menu items from a campus cafeteria, add items to a cart, and place orders. The system tracks orders and provides order history to users.

The application uses a modern React frontend with a Node.js/Express backend. It's built with a component-based architecture using shadcn/ui components and Tailwind CSS for styling. Data is managed using Zustand for client-side state management and will use Drizzle ORM for database interactions.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

- **Framework**: React with TypeScript
- **Routing**: Wouter for lightweight client-side routing
- **State Management**: Zustand for global state (cart, orders, theme)
- **UI Components**: shadcn/ui with Tailwind CSS for styling
- **Data Fetching**: TanStack Query (React Query) for API interactions

The frontend follows a component-based architecture with reusable UI components. State management is split into domain-specific stores (cart, orders, theme) using Zustand to maintain a single source of truth for each domain.

### Backend Architecture

- **Framework**: Express.js on Node.js
- **API Style**: RESTful
- **Database ORM**: Drizzle ORM
- **Session Management**: Will use connect-pg-simple for PostgreSQL session storage

The backend follows a layered architecture:
1. **Route Layer**: Request handling and endpoint definition
2. **Service Layer**: Business logic implementation
3. **Data Layer**: Database interactions through storage interface

### Data Storage

- **Database**: Will use PostgreSQL (Neon Serverless via `@neondatabase/serverless`)
- **ORM**: Drizzle ORM for type-safe database access
- **Schema**: Simple schema with users table defined, expandable for menu items and orders

### Authentication/Authorization

Currently, the system has a basic user schema setup with username/password fields, but the authentication system is not fully implemented. This area needs development to add:

1. User registration and login flows
2. Password hashing and security
3. Session management

## Key Components

### Frontend Components

1. **Layout Components**:
   - `Navbar`: Application navigation with cart toggle
   - `CartDrawer`: Slide-in cart with order management

2. **Page Components**:
   - `MenuPage`: Main page displaying food items with category filtering
   - `OrdersPage`: User order history and reordering capability

3. **UI Components**:
   - `FoodCard`: Displays menu item with add to cart functionality
   - `OrderCard`: Displays order with reorder capability
   - `CartItem`: Individual cart item with quantity controls

4. **State Management**:
   - `cart-store`: Manages cart items, quantities, and totals
   - `order-store`: Manages order history with persistence
   - `theme-store`: Handles theme switching (light/dark)

### Backend Components

1. **Server Setup**:
   - Express application with middleware configuration
   - Request/response logging

2. **API Routes**:
   - Route definition and registration (to be implemented)

3. **Storage Interface**:
   - Abstract storage interface allowing swappable implementations
   - Currently using in-memory storage as placeholder
   - Will transition to PostgreSQL with Drizzle ORM

4. **Database Schema**:
   - Initial user schema defined with Drizzle
   - Extensible for menu items and orders

## Data Flow

1. **Menu Browsing**:
   - Currently uses static data in `menu-items.ts`
   - Future implementation will fetch menu data from API

2. **Cart Management**:
   - Add/remove/update cart items through Zustand store
   - Cart persists during session
   - Cart calculates subtotal, tax, and total

3. **Order Placement**:
   - Order created from cart items
   - Order stored in order history via Zustand
   - Order history persisted to localStorage
   - Future implementation will send order to API

4. **Order History**:
   - Orders retrieved from localStorage currently
   - Future implementation will fetch from API
   - Reordering populates cart with previous order items

## External Dependencies

### Frontend Dependencies

- **UI Libraries**: shadcn/ui, Tailwind CSS, Radix UI primitives
- **State Management**: Zustand, TanStack Query
- **Routing**: Wouter
- **Icons**: Remix Icons
- **Date Handling**: date-fns

### Backend Dependencies

- **Web Framework**: Express.js
- **Database**: Drizzle ORM with Neon PostgreSQL (@neondatabase/serverless)
- **Session Management**: connect-pg-simple
- **Validation**: Zod with drizzle-zod integration
- **Development**: Vite, esbuild, tsx

## Deployment Strategy

The application is configured for deployment on Replit with a combined build strategy:

1. **Development Mode**:
   - Uses `npm run dev` to run the Express server with Vite dev server
   - Provides hot module reloading and development enhancements

2. **Production Build**:
   - Frontend: Vite builds static assets to `dist/public`
   - Backend: esbuild compiles TypeScript to JavaScript
   - Combined: Single Node.js process serves both API and static files

3. **Database Provisioning**:
   - Will use Replit PostgreSQL database module
   - Database URL expected in environment variable `DATABASE_URL`
   - Drizzle migrations can be run with `npm run db:push`

## Upcoming Development Tasks

1. **Backend API Implementation**:
   - Complete RESTful API endpoints for menu items, cart, and orders
   - Implement authentication and authorization

2. **Database Integration**:
   - Migrate from in-memory storage to PostgreSQL
   - Complete schema definition for menu items and orders
   - Implement data access patterns

3. **Frontend Enhancements**:
   - Connect to backend API using TanStack Query
   - Add user authentication UI
   - Implement profile management

4. **Testing**:
   - Add unit tests for components and stores
   - Add integration tests for API endpoints
   - Add end-to-end tests for critical flows