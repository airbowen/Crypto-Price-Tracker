﻿# Crypto Price Tracker

![Crypto Price Tracker]

![4b96cf29dd6dc415143395eb3e92dea](https://github.com/user-attachments/assets/27689548-3ffa-4dd3-9a5a-0d9bc70ee1ff)

A modern cryptocurrency price tracking application built with Next.js that displays real-time prices of cryptocurrencies using the CoinGecko API.

## 🚀 Features

- **Live Cryptocurrency Data**: Real-time price updates from CoinGecko API
- **Top Cryptocurrencies**: Displays the top 5 cryptocurrencies by market cap
- **Search Functionality**: Filter cryptocurrencies by name or symbol
- **Manual Refresh**: Update prices on demand with a refresh button
- **Responsive Design**: Works seamlessly on mobile, tablet, and desktop
- **Loading States**: Skeleton loaders provide visual feedback during data fetching
- **Error Handling**: Graceful handling of API errors and rate limiting
- **Detailed Information**: View price, 24h change, market cap, and volume

## 🛠️ Technologies

- **[Next.js](https://nextjs.org/)**: React framework with App Router
- **[React Query](https://tanstack.com/query/latest)**: For data fetching, caching, and state management
- **[Tailwind CSS](https://tailwindcss.com/)**: For styling and responsive design
- **[shadcn/ui](https://ui.shadcn.com/)**: For UI components
- **[TypeScript](https://www.typescriptlang.org/)**: For type safety
- **[CoinGecko API](https://www.coingecko.com/en/api/documentation)**: For cryptocurrency data
- **[Lucide React](https://lucide.dev/icons/)**: For icons

## 📋 Prerequisites

Before you begin, ensure you have the following installed:
- [Node.js](https://nodejs.org/) (v18 or later)
- npm (v8 or later) or [yarn](https://yarnpkg.com/) (v1.22 or later)



# Crypto Price Tracker Documentation

## Introduction
Welcome to the documentation for the Crypto Price Tracker project. This guide provides detailed instructions on setting up the project, integrating APIs, managing state, and addressing challenges faced during development.

---

## Project Setup Guide

### Prerequisites
Ensure you have the following installed:
- Node.js (LTS version recommended)
- npm or yarn
- Expo CLI (for mobile app)

### Setting Up the Web App
1. Clone the repository:
   ```sh
   git clone https://github.com/airbowen/Crypto-Price-Tracker.git
   cd Crypto-Price-Tracker/web
   cd webapp
   ```
2. Install dependencies:
   ```sh
   npm install --force
   ```
3. Start the development server:
   ```sh
   npm run dev
   ```
4. Open the browser and navigate to `http://localhost:3000`.

### Setting Up the Mobile App
1. Navigate to the mobile app directory:
   ```sh
   cd ../mobile
   ```
2. Install dependencies:
   ```sh
   npm install
   ```
3. Start the development server:
   ```sh
   expo start
   ```
4. Scan the QR code with the Expo Go app to run on a physical device.

---

## API Integration Details

### Fetching Data
The project integrates with a public cryptocurrency API to retrieve real-time prices. Data fetching is handled using `fetch` in JavaScript.

#### Example API Call
```js
const fetchCryptoPrices = async () => {
  const response = await fetch('https://api.coingecko.com/api/v3/simple/price?ids=bitcoin,ethereum&vs_currencies=usd');
  const data = await response.json();
  return data;
};
```

### Updating Data
To ensure real-time updates, the app uses polling at regular intervals.

```js
useEffect(() => {
  const interval = setInterval(fetchCryptoPrices, 30000);
  return () => clearInterval(interval);
}, []);
```

---

## State Management Explanation

### Why React Query?
We chose React Query for efficient data fetching and caching. It simplifies API requests and keeps the UI in sync with the latest data.

#### Example with React Query
```js
import { useQuery } from 'react-query';

const useCryptoPrices = () => {
  return useQuery('cryptoPrices', fetchCryptoPrices, {
    refetchInterval: 30000,
  });
};
```

### Alternative State Management Approaches
- **Zustand**: If fine-grained state control is needed.
- **Context API**: Suitable for global state but lacks built-in caching.

---

## Challenges & Solutions

### 1. API Rate Limits
- **Challenge:** The public API has rate limits, restricting frequent requests.
- **Solution:** Implemented caching using React Query and reduced polling frequency.

### 2. UI Performance
- **Challenge:** Frequent re-renders caused performance issues.
- **Solution:** Used memoization (`useMemo`, `useCallback`) to optimize rendering.

### 3. Cross-Platform Differences
- **Challenge:** Styling inconsistencies between web and mobile.
- **Solution:** Used Tailwind CSS for web and React Native’s StyleSheet API for mobile.

---

## Conclusion
This documentation provides an overview of setting up and managing the Crypto Price Tracker project. For further assistance, feel free to raise issues on the GitHub repository.

Happy coding! 🚀

