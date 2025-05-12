# Musicplayer
from PySide6.QtWidgets import QApplication, QWidget, QPushButton, QVBoxLayout, QFileDialog
from PySide6.QtMultimedia import QMediaPlayer, QAudioOutput
from PySide6.QtCore import QUrl
class MusicPlayer(QWidget):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("Music Player")
        self.setGeometry(100, 100, 100, 100)
        self.player = QMediaPlayer()
        self.audio_output = QAudioOutput()
        self.player.setAudioOutput(self.audio_output)
        self.play_button = QPushButton("Play")
        self.stop_button = QPushButton("Stop")
        self.open_button = QPushButton("Open File")
        layout = QVBoxLayout()
        layout.addWidget(self.open_button)
        layout.addWidget(self.play_button)
        layout.addWidget(self.stop_button)
        self.setLayout(layout)
        self.open_button.clicked.connect(self.open_file)
        self.play_button.clicked.connect(self.player.play)
        self.stop_button.clicked.connect(self.player.stop)
    def open_file(self):
        file_path, _ = QFileDialog.getOpenFileName(self, "Open Audio File", "", "Audio Files (*.mp3 *.wav)")
        if file_path:
            self.player.setSource(QUrl.fromLocalFile(file_path))
            self.audio_output.setVolume(0.6)
if __name__ == "__main__":
    app = QApplication([])
    player = MusicPlayer()
    player.show()
    app.exec()
