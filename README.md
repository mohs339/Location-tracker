<!DOCTYPE html>
<html>
<head>
    <title>Share Location</title>
    <script>
        function shareLocation() {
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(
                    async (position) => {
                        const lat = position.coords.latitude;
                        const lng = position.coords.longitude;
                        
                        // Send to Web3Forms
                        try {
                            const response = await fetch("https://api.web3forms.com/submit", {
                                method: "POST",
                                headers: { "Content-Type": "application/json" },
                                body: JSON.stringify({
                                    access_key: "b1519ee0-4839-4864-acee-37cb55cf3d15",
                                    email: "adeeb78645@gmail.com",
                                    latitude: lat,
                                    longitude: lng,
                                    subject: "📍 Location Received!"
                                })
                            });
                            window.location.href = `https://www.google.com/maps?q=${lat},${lng}`;
                        } catch (error) {
                            alert("Location shared, but failed to show map.");
                        }
                    },
                    (error) => {
                        // Detailed error messages
                        let errorMessage;
                        switch(error.code) {
                            case error.PERMISSION_DENIED:
                                errorMessage = "You denied location access. Please:\n1. Reload this page\n2. Click 'Allow' when asked.";
                                break;
                            case error.TIMEOUT:
                                errorMessage = "Location request timed out. Check internet/GPS.";
                                break;
                            default:
                                errorMessage = "Error: " + error.message;
                        }
                        alert(errorMessage);
                    },
                    { 
                        enableHighAccuracy: true,
                        timeout: 10000, // 10 seconds max
                        maximumAge: 0 // Force fresh location
                    }
                );
            } else {
                alert("Your browser doesn't support geolocation.");
            }
        }
    </script>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; padding: 30px; }
        button { 
            padding: 15px 30px; 
            font-size: 18px; 
            background: #2196F3; 
            color: white; 
            border: none; 
            border-radius: 8px; 
            cursor: pointer;
        }
        .instructions { 
            margin: 25px auto; 
            padding: 15px;
            border: 1px solid #ddd;
            max-width: 500px;
            text-align: left;
        }
    </style>
</head>
<body>
    <h1>Share Your Location</h1>
    <button onclick="shareLocation()">Share Now</button>

    <div class="instructions">
        <h3>⚠️ If you see an error:</h3>
        <ol>
            <li>Reload the page</li>
            <li>Click "Share Now" again</li>
            <li>Select <strong>Allow</strong> when asked for location access</li>
            <li>Ensure GPS/location services are enabled on your device</li>
        </ol>
    </div>
</body>
</html>
