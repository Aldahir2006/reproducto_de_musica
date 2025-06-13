import javazoom.jl.player.advanced.AdvancedPlayer;
import javax.swing.*; // Importa componentes de interfaz gráfica de Swing
import java.awt.*; // Importa clases para diseño visual y componentes (layout)
// Importa clases para manejar archivos
import java.io.File;
import java.io.FileInputStream;

public class MusicPlayerSimple extends JFrame { // Clase principal que extiende JFrame para crear la ventana de la aplicación

    private AdvancedPlayer player; // Objeto para reproducir archivos MP3
    private Thread playerThread;  // Hilo para reproducir la canción sin congelar la interfaz
    private boolean isPaused = false;  // Bandera para saber si la canción está pausada
    private String filePath = null; // Ruta del archivo MP3 seleccionado

    // Ruta predeterminada donde se encuentran las canciones
    private final String defaultMusicDirectory = "C:\\Users\\Denilson\\IdeaProjects\\untitled\\musica";

    // Constructor del reproductor
    public MusicPlayerSimple() {
        setTitle("Reproductor MP3"); // Título de la ventana
        setSize(400, 200);  // Tamaño de la ventana
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setLayout(new FlowLayout()); // Usa diseño FlowLayout

        JButton chooseButton = new JButton("Elegir Canción");
        JButton playButton = new JButton("Reproducir");
        JButton pauseButton = new JButton("Pausar");
        JButton resumeButton = new JButton("Reanudar");
        JButton stopButton = new JButton("Detener");

        chooseButton.addActionListener(e -> chooseFile());
        playButton.addActionListener(e -> play());
        pauseButton.addActionListener(e -> pause());
        resumeButton.addActionListener(e -> resume());
        stopButton.addActionListener(e -> stop());

        add(chooseButton);
        add(playButton);
        add(pauseButton);
        add(resumeButton);
        add(stopButton);
    }

    // Método para elegir un archivo MP3 desde el explorador
    private void chooseFile() {
        JFileChooser fileChooser = new JFileChooser(new File(defaultMusicDirectory)); // carpeta inicial
        fileChooser.setDialogTitle("Selecciona una canción MP3");
        int result = fileChooser.showOpenDialog(this);
        if (result == JFileChooser.APPROVE_OPTION) {
            File selectedFile = fileChooser.getSelectedFile();
            filePath = selectedFile.getAbsolutePath();
            JOptionPane.showMessageDialog(this, "Archivo seleccionado: " + selectedFile.getName());
        }
    }

    // Método para reproducir la canción seleccionada
    private void play() {
        stop();
        isPaused = false;

        if (filePath == null) {
            JOptionPane.showMessageDialog(this, "Primero debes seleccionar una canción.");
            return;
        }

        // Crea un hilo para la reproducción
        playerThread = new Thread(() -> {
            try {
                FileInputStream fis = new FileInputStream(filePath);
                player = new AdvancedPlayer(fis);
                System.out.println("▶ Reproduciendo: " + filePath);
                player.play();
            } catch (Exception e) {
                JOptionPane.showMessageDialog(this, "Error al reproducir: " + e.getMessage());
            }
        });
        playerThread.start();
    }

    private void pause() {
        if (player != null) {
            System.out.println("⏸ Pausado");
            isPaused = true;
            stop();
        }
    }

    private void resume() {
        if (isPaused) {
            System.out.println("▶ Reanudando...");
            play();
            isPaused = false;
        }
    }

    private void stop() {
        if (player != null) {
            System.out.println("⏹ Detenido");
            player.close();
        }
        if (playerThread != null) {
            playerThread.interrupt();
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new MusicPlayerSimple().setVisible(true));
    }
}
