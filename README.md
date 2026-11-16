# Lokesh
Jarvis is here to take your commands

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>JARVIS AI</title>

<style>
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    background: #020912;
    color: #00eaff;
    font-family: Arial, sans-serif;
    text-align: center;
}

header {
    padding: 25px;
    font-size: 28px;
    letter-spacing: 5px;
    text-shadow: 0 0 15px #00eaff;
}

.circle {
    width: 190px;
    height: 190px;
    border: 4px solid #00eaff;
    border-radius: 50%;
    margin: 45px auto 25px;
    box-shadow: 0 0 20px #00eaff,
                inset 0 0 25px #00eaff;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 45px;
    animation: glow 2s infinite alternate;
}

@keyframes glow {
    from { box-shadow: 0 0 10px #00eaff; }
    to { box-shadow: 0 0 35px #00eaff; }
}

#clock {
    font-size: 25px;
    margin: 20px;
}

#status {
    color: #ffffff;
    margin: 20px;
}

button {
    background: transparent;
    border: 2px solid #00eaff;
    color: #00eaff;
    padding: 15px 25px;
    margin: 10px;
    border-radius: 30px;
    font-size: 16px;
}

button:active {
    background: #00eaff;
    color: black;
}

input {
    background: #061b2b;
    border: 1px solid #00eaff;
    color: white;
    padding: 15px;
    width: 75%;
    border-radius: 20px;
    outline: none;
}

#response {
    padding: 20px;
    min-height: 60px;
    color: white;
}
</style>
</head>

<body>

<header>J.A.R.V.I.S</header>

<div class="circle">J</div>

<h3>JUST A RATHER VERY INTELLIGENT SYSTEM</h3>

<div id="clock"></div>

<p id="status">SYSTEM ONLINE</p>

<div>
<button onclick="startListening()">🎤 SPEAK</button>
<button onclick="speak('At your service, sir.')">🔊 TEST VOICE</button>
</div>

<br>

<input id="command"
placeholder="Enter your command...">

<button onclick="runCommand()">SEND</button>

<div id="response">Welcome back, Sir.</div>

<script>

function updateClock() {
    document.getElementById("clock").innerHTML =
    new Date().toLocaleTimeString();
}

setInterval(updateClock, 1000);
updateClock();

function speak(text) {
    speechSynthesis.cancel();

    let speech = new SpeechSynthesisUtterance(text);
    speech.lang = "en-IN";
    speech.rate = 0.9;
    speech.pitch = 0.85;

    speechSynthesis.speak(speech);

    document.getElementById("response").innerText = text;
}

function runCommand() {
    let command = document
    .getElementById("command")
    .value.toLowerCase().trim();

    if (command.includes("hello")) {
        speak("Hello Sir. JARVIS is ready.");
    }

    else if (command.includes("time")) {
        speak("The time is " +
        new Date().toLocaleTimeString());
    }

    else if (command.includes("date")) {
        speak("Today's date is " +
        new Date().toDateString());
    }

    else if (command.includes("your name")) {
        speak("I am JARVIS, your personal assistant.");
    }

    else if (command.includes("who am i")) {
        speak("You are my creator, Sir.");
    }

    else if (command.includes("how are you")) {
        speak("All systems are functioning normally, Sir.");
    }

    else if (command.includes("stop")) {
        speechSynthesis.cancel();
        speak("Voice system stopped.");
    }

    else {
        speak("Sorry Sir. I don't understand that command yet.");
    }
}

function startListening() {

    const Recognition =
    window.SpeechRecognition ||
    window.webkitSpeechRecognition;

    if (!Recognition) {
        speak("Speech recognition is not supported in this browser.");
        return;
    }

    let recognition = new Recognition();

    recognition.lang = "en-IN";
    recognition.continuous = false;
    recognition.interimResults = false;

    document.getElementById("status").innerText =
    "LISTENING...";

    recognition.onresult = function(event) {
        let text = event.results[0][0].transcript;

        document.getElementById("command").value = text;

        runCommand();
    };

    recognition.onerror = function() {
        document.getElementById("status").innerText =
        "VOICE ERROR";
    };

    recognition.onend = function() {
        document.getElementById("status").innerText =
        "SYSTEM ONLINE";
    };

    recognition.start();
}

</script>

</body>
</html>
