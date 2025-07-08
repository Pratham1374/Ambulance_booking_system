<!DOCTYPE html>
<html lang="en">
<head>
    <base target="_self">
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MediRescue - Online Ambulance Booking</title>
    <meta name="description" content="Book emergency ambulances online with real-time tracking">
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        primary: "#e11d48",
                        secondary: "#9f1239",
                        accent: "#f43f5e"
                    },
                    fontFamily: {
                        sans: ['Poppins', 'sans-serif']
                    }
                }
            }
        }
    </script>
    <style>
        .map-container {
            height: 300px;
            width: 100%;
            background-color: #e5e7eb;
            position: relative;
            overflow: hidden;
        }
        .map-placeholder {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            text-align: center;
        }
    </style>
</head>
<body class="font-sans bg-gray-50">
    <!-- Header/Navigation -->
    <header class="bg-white shadow-md sticky top-0 z-50">
        <nav class="container mx-auto px-4 py-3 flex justify-between items-center">
            <div class="flex items-center">
                <div class="bg-red-600 text-white p-2 rounded-full mr-3">
                    <i class="fas fa-ambulance text-xl"></i>
                </div>
                <a href="#" class="text-2xl font-bold text-gray-800">MediRescue</a>
            </div>
            <div class="hidden md:flex space-x-8">
                <a href="#" class="text-red-600 font-medium">Home</a>
                <a href="#book" class="text-gray-600 hover:text-red-600">Book Ambulance</a>
                <a href="#track" class="text-gray-600 hover:text-red-600">Track Ambulance</a>
                <a href="#about" class="text-gray-600 hover:text-red-600">About Us</a>
                <a href="#contact" class="text-gray-600 hover:text-red-600">Contact</a>
            </div>
            <div class="md:hidden">
                <button id="menu-toggle" class="text-gray-600 focus:outline-none">
                    <i class="fas fa-bars text-2xl"></i>
                </button>
            </div>
        </nav>
        <!-- Mobile Menu -->
        <div id="mobile-menu" class="hidden md:hidden bg-white py-2 px-4 shadow-lg">
            <a href="#" class="block py-2 text-red-600 font-medium">Home</a>
            <a href="#book" class="block py-2 text-gray-600 hover:text-red-600">Book Ambulance</a>
            <a href="#track" class="block py-2 text-gray-600 hover:text-red-600">Track Ambulance</a>
            <a href="#about" class="block py-2 text-gray-600 hover:text-red-600">About Us</a>
            <a href="#contact" class="block py-2 text-gray-600 hover:text-red-600">Contact</a>
            <a href="#login" class="block py-2 text-gray-600 hover:text-red-600">Admin Login</a>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="bg-gradient-to-r from-red-600 to-red-800 text-white py-16 md:py-24">
        <div class="container mx-auto px-4 flex flex-col md:flex-row items-center">
            <div class="md:w-1/2 mb-8 md:mb-0">
                <h1 class="text-4xl md:text-5xl font-bold mb-4">Emergency Ambulance Services</h1>
                <p class="text-xl mb-6">Fast, reliable ambulance services when you need them most. Book online or call our emergency hotline.</p>
                <div class="flex flex-col sm:flex-row gap-4">
                    <a href="#book" class="bg-white text-red-600 font-bold py-3 px-6 rounded-lg hover:bg-gray-100 text-center transition duration-300">
                        Book Ambulance Now
                    </a>
                    <div class="bg-black bg-opacity-20 py-3 px-6 rounded-lg flex items-center justify-center">
                        <i class="fas fa-phone-alt mr-2"></i>
                        <span class="font-bold">Emergency: 108</span>
                    </div>
                </div>
            </div>
            <div class="md:w-1/2 flex justify-center">
                <img src="https://picsum.photos/600/400?random=1" alt="Ambulance in service" class="rounded-lg shadow-xl max-w-full h-auto">
            </div>
        </div>
    </section>

    <!-- Booking Form Section -->
    <section id="book" class="py-16 bg-white">
        <div class="container mx-auto px-4">
            <h2 class="text-3xl font-bold text-center mb-12 text-gray-800">Book an Ambulance</h2>
            <div class="max-w-3xl mx-auto bg-gray-50 rounded-xl shadow-md overflow-hidden p-6 md:p-8">
                <form id="booking-form">
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label for="name" class="block text-gray-700 font-medium mb-2">Full Name</label>
                            <input type="text" id="name" name="name" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-500 focus:border-red-500 outline-none transition">
                        </div>
                        <div>
                            <label for="phone" class="block text-gray-700 font-medium mb-2">Contact Number</label>
                            <input type="tel" id="phone" name="phone" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-500 focus:border-red-500 outline-none transition">
                        </div>
                        <div class="md:col-span-2">
                            <label for="pickup" class="block text-gray-700 font-medium mb-2">Pickup Address</label>
                            <div class="map-container mb-4 rounded-lg overflow-hidden">
                                <div class="map-placeholder">
                                    <i class="fas fa-map-marker-alt text-4xl text-red-600 mb-2"></i>
                                    <p class="text-gray-600">Google Maps integration would appear here</p>
                                </div>
                            </div>
                            <textarea id="pickup" name="pickup" rows="2" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-500 focus:border-red-500 outline-none transition"></textarea>
                        </div>
                        <div class="md:col-span-2">
                            <label for="drop" class="block text-gray-700 font-medium mb-2">Drop Location (Hospital/Address)</label>
                            <input type="text" id="drop" name="drop" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-500 focus:border-red-500 outline-none transition">
                        </div>
                        <div>
                            <label for="emergency" class="block text-gray-700 font-medium mb-2">Emergency Type</label>
                            <select id="emergency" name="emergency" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-500 focus:border-red-500 outline-none transition">
                                <option value="">Select Emergency Type</option>
                                <option value="accident">Accident</option>
                                <option value="heart">Heart Attack</option>
                                <option value="stroke">Stroke</option>
                                <option value="maternity">Maternity</option>
                                <option value="respiratory">Respiratory Emergency</option>
                                <option value="other">Other Medical Emergency</option>
                            </select>
                        </div>
                        <div>
                            <label for="ambulance" class="block text-gray-700 font-medium mb-2">Ambulance Type</label>
                            <select id="ambulance" name="ambulance" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-500 focus:border-red-500 outline-none transition">
                                <option value="">Select Ambulance Type</option>
                                <option value="basic">Basic Life Support</option>
                                <option value="advanced">Advanced Life Support</option>
                                <option value="icu">ICU Ambulance</option>
                                <option value="neonatal">Neonatal Ambulance</option>
                                <option value="air">Air Ambulance</option>
                            </select>
                        </div>
                        <div>
                            <label for="date" class="block text-gray-700 font-medium mb-2">Date</label>
                            <input type="date" id="date" name="date" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-500 focus:border-red-500 outline-none transition">
                        </div>
                        <div>
                            <label for="time" class="block text-gray-700 font-medium mb-2">Time</label>
                            <input type="time" id="time" name="time" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-500 focus:border-red-500 outline-none transition">
                        </div>
                    </div>
                    <div class="mt-8">
                        <button type="submit" class="w-full bg-red-600 hover:bg-red-700 text-white font-bold py-3 px-6 rounded-lg transition duration-300">
                            Book Ambulance Now
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </section>

    <!-- Ambulance Tracker Section -->
    <section id="track" class="py-16 bg-gray-50">
        <div class="container mx-auto px-4">
            <h2 class="text-3xl font-bold text-center mb-12 text-gray-800">Live Ambulance Tracker</h2>
            <div class="max-w-5xl mx-auto bg-white rounded-xl shadow-md overflow-hidden">
                <div class="p-6 md:p-8">
                    <div class="flex flex-col md:flex-row gap-6">
                        <div class="md:w-1/3">
                            <h3 class="text-xl font-semibold mb-4">Your Ambulance Status</h3>
                            <div class="bg-gray-100 p-4 rounded-lg mb-4">
                                <div class="flex justify-between items-center mb-2">
                                    <span class="font-medium">Booking ID:</span>
                                    <span class="font-mono">MR-58492</span>
                                </div>
                                <div class="flex justify-between items-center mb-2">
                                    <span class="font-medium">Ambulance:</span>
                                    <span>ICU Ambulance #A-42</span>
                                </div>
                                <div class="flex justify-between items-center mb-2">
                                    <span class="font-medium">Driver:</span>
                                    <span>Rajesh Kumar</span>
                                </div>
                                <div class="flex justify-between items-center">
                                    <span class="font-medium">Contact:</span>
                                    <span>+91 98765 43210</span>
                                </div>
                            </div>
                            <div class="space-y-4">
                                <div class="flex items-start">
                                    <div class="flex-shrink-0 pt-1">
                                        <div class="h-4 w-4 rounded-full bg-red-600"></div>
                                    </div>
                                    <div class="ml-3">
                                        <p class="text-sm font-medium text-gray-900">Ambulance dispatched</p>
                                        <p class="text-sm text-gray-500">5 minutes ago</p>
                                    </div>
                                </div>
                                <div class="flex items-start">
                                    <div class="flex-shrink-0 pt-1">
                                        <div class="h-4 w-4 rounded-full bg-yellow-500"></div>
                                    </div>
                                    <div class="ml-3">
                                        <p class="text-sm font-medium text-gray-900">En route to pickup location</p>
                                        <p class="text-sm text-gray-500">3 minutes ago</p>
                                    </div>
                                </div>
                                <div class="flex items-start">
                                    <div class="flex-shrink-0 pt-1">
                                        <div class="h-4 w-4 rounded-full bg-gray-300"></div>
                                    </div>
                                    <div class="ml-3">
                                        <p class="text-sm font-medium text-gray-900">Estimated arrival: 8 min</p>
                                        <p class="text-sm text-gray-500">Updated just now</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="md:w-2/3">
                            <div class="map-container rounded-lg overflow-hidden h-full">
                                <div class="map-placeholder">
                                    <i class="fas fa-map-marked-alt text-4xl text-red-600 mb-2"></i>
                                    <p class="text-gray-600">Live ambulance tracking would appear here</p>
                                    <p class="text-sm text-gray-500 mt-2">(GPS integration with real-time updates)</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Admin Login Section -->
    <section id="login" class="py-16 bg-white">
        <div class="container mx-auto px-4">
            <h2 class="text-3xl font-bold text-center mb-12 text-gray-800">Admin Login</h2>
            <div class="max-w-md mx-auto bg-gray-50 rounded-xl shadow-md overflow-hidden p-6 md:p-8">
                <form id="login-form">
                    <div class="mb-6">
                        <label for="username" class="block text-gray-700 font-medium mb-2">Username</label>
                        <input type="text" id="username" name="username" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-500 focus:border-red-500 outline-none transition">
                    </div>
                    <div class="mb-6">
                        <label for="password" class="block text-gray-700 font-medium mb-2">Password</label>
                        <input type="password" id="password" name="password" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-500 focus:border-red-500 outline-none transition">
                    </div>
                    <div class="flex items-center justify-between mb-6">
                        <div class="flex items-center">
                            <input id="remember" name="remember" type="checkbox" class="h-4 w-4 text-red-600 focus:ring-red-500 border-gray-300 rounded">
                            <label for="remember" class="ml-2 block text-sm text-gray-700">Remember me</label>
                        </div>
                        <a href="#" class="text-sm text-red-600 hover:text-red-800">Forgot password?</a>
                    </div>
                    <button type="submit" class="w-full bg-red-600 hover:bg-red-700 text-white font-bold py-3 px-6 rounded-lg transition duration-300">
                        Login
                    </button>
                </form>
            </div>
        </div>
    </section>

    <!-- About Us Section -->
    <section id="about" class="py-16 bg-gray-50">
        <div class="container mx-auto px-4">
            <h2 class="text-3xl font-bold text-center mb-12 text-gray-800">About MediRescue</h2>
            <div class="max-w-4xl mx-auto">
                <div class="flex flex-col md:flex-row gap-8 items-center mb-12">
                    <div class="md:w-1/2">
                        <img src="https://picsum.photos/600/400?random=2" alt="Our ambulance fleet" class="rounded-lg shadow-lg w-full">
                    </div>
                    <div class="md:w-1/2">
                        <h3 class="text-2xl font-semibold mb-4 text-gray-800">Our Mission</h3>
                        <p class="text-gray-600 mb-4">MediRescue is committed to providing fast, reliable emergency medical transportation services to communities across the region. Our mission is to save lives by reducing emergency response times through advanced technology and highly trained medical professionals.</p>
                        <p class="text-gray-600">Founded in 2010, we've grown to become the most trusted ambulance service provider, with a fleet of over 200 vehicles serving 15+ cities.</p>
                    </div>
                </div>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                    <div class="bg-white p-6 rounded-lg shadow-md">
                        <div class="text-red-600 text-3xl mb-4">
                            <i class="fas fa-bolt"></i>
                        </div>
                        <h4 class="text-xl font-semibold mb-2">Fast Response</h4>
                        <p class="text-gray-600">Average response time of under 12 minutes in urban areas.</p>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-md">
                        <div class="text-red-600 text-3xl mb-4">
                            <i class="fas fa-user-md"></i>
                        </div>
                        <h4 class="text-xl font-semibold mb-2">Trained Professionals</h4>
                        <p class="text-gray-600">EMTs and paramedics with advanced medical training.</p>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow-md">
                        <div class="text-red-600 text-3xl mb-4">
                            <i class="fas fa-shield-alt"></i>
                        </div>
                        <h4 class="text-xl font-semibold mb-2">Advanced Equipment</h4>
                        <p class="text-gray-600">State-of-the-art medical equipment in all our ambulances.</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Contact Us Section -->
    <section id="contact" class="py-16 bg-white">
        <div class="container mx-auto px-4">
            <h2 class="text-3xl font-bold text-center mb-12 text-gray-800">Contact Us</h2>
            <div class="max-w-6xl mx-auto">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                    <div>
                        <h3 class="text-2xl font-semibold mb-4 text-gray-800">Emergency Contacts</h3>
                        <div class="space-y-4">
                            <div class="flex items-start">
                                <div class="flex-shrink-0 text-red-600 mt-1">
                                    <i class="fas fa-phone-alt"></i>
                                </div>
                                <div class="ml-3">
                                    <p class="text-lg font-medium">24/7 Emergency Hotline</p>
                                    <p class="text-gray-600">108 (Toll-free)</p>
                                </div>
                            </div>
                            <div class="flex items-start">
                                <div class="flex-shrink-0 text-red-600 mt-1">
                                    <i class="fas fa-phone-alt"></i>
                                </div>
                                <div class="ml-3">
                                    <p class="text-lg font-medium">Customer Support</p>
                                    <p class="text-gray-600">+91 1800 123 4567</p>
                                </div>
                            </div>
                            <div class="flex items-start">
                                <div class="flex-shrink-0 text-red-600 mt-1">
                                    <i class="fas fa-envelope"></i>
                                </div>
                                <div class="ml-3">
                                    <p class="text-lg font-medium">Email</p>
                                    <p class="text-gray-600">support@medirescue.com</p>
                                </div>
                            </div>
                            <div class="flex items-start">
                                <div class="flex-shrink-0 text-red-600 mt-1">
                                    <i class="fas fa-map-marker-alt"></i>
                                </div>
                                <div class="ml-3">
                                    <p class="text-lg font-medium">Headquarters</p>
                                    <p class="text-gray-600">123 Medical Plaza, Health City, Bangalore - 560001</p>
                                </div>
                            </div>
                        </div>
                        <div class="mt-8">
                            <h4 class="text-xl font-semibold mb-4">Follow Us</h4>
                            <div class="flex space-x-4">
                                <a href="#" class="text-red-600 hover:text-red-800 text-2xl">
                                    <i class="fab fa-facebook"></i>
                                </a>
                                <a href="#" class="text-red-600 hover:text-red-800 text-2xl">
                                    <i class="fab fa-twitter"></i>
                                </a>
                                <a href="#" class="text-red-600 hover:text-red-800 text-2xl">
                                    <i class="fab fa-instagram"></i>
                                </a>
                                <a href="#" class="text-red-600 hover:text-red-800 text-2xl">
                                    <i class="fab fa-linkedin"></i>
                                </a>
                            </div>
                        </div>
                    </div>
                    <div>
                        <h3 class="text-2xl font-semibold mb-4 text-gray-800">Send Us a Message</h3>
                        <form id="contact-form" class="space-y-4">
                            <div>
                                <label for="contact-name" class="block text-gray-700 font-medium mb-2">Your Name</label>
                                <input type="text" id="contact-name" name="name" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-500 focus:border-red-500 outline-none transition">
                            </div>
                            <div>
                                <label for="contact-email" class="block text-gray-700 font-medium mb-2">Email Address</label>
                                <input type="email" id="contact-email" name="email" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-500 focus:border-red-500 outline-none transition">
                            </div>
                            <div>
                                <label for="contact-subject" class="block text-gray-700 font-medium mb-2">Subject</label>
                                <input type="text" id="contact-subject" name="subject" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-500 focus:border-red-500 outline-none transition">
                            </div>
                            <div>
                                <label for="contact-message" class="block text-gray-700 font-medium mb-2">Message</label>
                                <textarea id="contact-message" name="message" rows="4" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-500 focus:border-red-500 outline-none transition"></textarea>
                            </div>
                            <button type="submit" class="w-full bg-red-600 hover:bg-red-700 text-white font-bold py-3 px-6 rounded-lg transition duration-300">
                                Send Message
                            </button>
