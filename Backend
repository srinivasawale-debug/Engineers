const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');
require('dotenv').config();

const workerRoutes = require('./routes/workerRoutes');
const jobRoutes = require('./routes/jobRoutes');

const app = express();

// Middleware Functionality
app.use(cors());
app.use(express.json());

// Main API Routes
app.use('/api/workers', workerRoutes);
app.use('/api/jobs', jobRoutes);

// Fallback error handling
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).json({ message: 'Something went wrong!', error: err.message });
});

// Database connection Setup
const PORT = process.env.PORT || 5000;
const MONGO_URI = process.env.MONGO_URI || 'mongodb://127.0.0.1:27017/rozgarsaathi';

mongoose.connect(MONGO_URI)
    .then(() => {
        console.log('✅ Connected to MongoDB successfully');
        app.listen(PORT, () => {
            console.log(`🚀 Server is running on port ${PORT}`);
            console.log(`Endpoint 1: http://localhost:${PORT}/api/workers`);
            console.log(`Endpoint 2: http://localhost:${PORT}/api/jobs`);
        });
    })
    .catch((err) => {
        console.error('❌ Error connecting to MongoDB:', err.message);
        console.log('Please ensure MongoDB is installed and running locally on port 27017.');
    });
