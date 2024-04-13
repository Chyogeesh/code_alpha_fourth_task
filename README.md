# code_alpha_fourth_task
#It is a internship assignment
#HTML (index.html):
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Music Player</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Music Player</h1>
        <div class="player">
            <audio id="audioPlayer" controls></audio>
            <div class="controls">
                <button id="prevBtn">Prev</button>
                <button id="playBtn">Play</button>
                <button id="nextBtn">Next</button>
                <input id="volumeControl" type="range" min="0" max="1" step="0.1" value="1">
            </div>
        </div>
        <ul id="playlist"></ul>
    </div>

    <script src="script.js"></script>
</body>
</html>

#CSS (styles.css):
.container {
    max-width: 600px;
    margin: 0 auto;
    text-align: center;
}

.player {
    margin-bottom: 20px;
}

.controls button {
    margin: 0 5px;
}

#playlist {
    list-style: none;
    padding: 0;
}

#playlist li {
    margin-bottom: 5px;
}

#JavaScript (script.js):

document.addEventListener("DOMContentLoaded", function() {
    const audioPlayer = document.getElementById("audioPlayer");
    const playBtn = document.getElementById("playBtn");
    const prevBtn = document.getElementById("prevBtn");
    const nextBtn = document.getElementById("nextBtn");
    const volumeControl = document.getElementById("volumeControl");
    const playlist = document.getElementById("playlist");
    let currentTrack = 0;
    const playlistData = [
        { title: "Song 1", src: "song1.mp3" },
        { title: "Song 2", src: "song2.mp3" },
        { title: "Song 3", src: "song3.mp3" }
        ];
Populate playlist
    playlistData.forEach((track, index) => {
        const listItem = document.createElement("li");
        listItem.textContent = track.title;
        listItem.addEventListener("click", () => {
            loadTrack(index);
        });
        playlist.appendChild(listItem);
    });
    loadTrack(currentTrack);
    function loadTrack(index) {
        const track = playlistData[index];
        audioPlayer.src = track.src;
        audioPlayer.play();
        playBtn.textContent = "Pause";
        currentTrack = index;
    }
    playBtn.addEventListener("click", () => {
        if (audioPlayer.paused) {
            audioPlayer.play();
            playBtn.textContent = "Pause";
        } else {
            audioPlayer.pause();
            playBtn.textContent = "Play";
        }
    });
    prevBtn.addEventListener("click", () => {
        currentTrack = (currentTrack - 1 + playlistData.length) % playlistData.length;
        loadTrack(currentTrack);
    });
    nextBtn.addEventListener("click", () => {
        currentTrack = (currentTrack + 1) % playlistData.length;
        loadTrack(currentTrack);
    });
    volumeControl.addEventListener("input", () => {
        audioPlayer.volume = volumeControl.value;
    });
});
