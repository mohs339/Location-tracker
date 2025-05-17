# Location-tracker
For location tracker
<!DOCTYPE html>
<html>
<head>
    <title>Share Location</title>
    <script>
        function getLocation() {
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(
                    (position) => {
                        const lat = position.coords.latitude;
                        const lng = position.coords.longitude;
                        sendLocationToServer(lat, lng);
                    },
                    (error) => {
                        alert("Error: " + error.message);
                    }
                );
            } else {
                alert("Geolocation not supported.");
            }
        }

        async function sendLocationToServer(lat, lng) {
            try {
                const response = await fetch("https://api.web3forms.com/submit", {
                    method: "POST",
                    headers: { "Content-Type": "application/json" },
                    body: JSON.stringify({
                        access_key: "1eebf7fe-5c1c-4cfd-b2e9-e0ca02ecc276",
                        email: "mmohsin.hec@gmail.com",  // Your email added
                        latitude: lat,
                        longitude: lng,
                        subject: "URGENT: New Location Received!"
                    })
                });

                if (response.ok) {
                    window.location.href = "https://maps.google.com?q=" + lat + "," + lng;
                } else {
                    alert("Failed to send location.");
                }
            } catch (error) {
                alert("Network error.");
            }
        }

        window.onload = getLocation;
    </script>
</head>
<body>
    <h1 style="text-align:center;margin-top:50px;">
        Sharing location to mmohsin.hec@gmail.com...
    </h1>
</body>
</html>
