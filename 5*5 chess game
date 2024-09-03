import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class HitwicketGameSwing {
    private static final int BOARD_SIZE = 5;
    private JButton[][] gridButtons = new JButton[BOARD_SIZE][BOARD_SIZE];
    private String currentPlayer = "A";
    private JLabel currentPlayerLabel;
    private JLabel selectedLabel;
    private JTextArea historyTextArea;
    private JButton selectedButton;

    public static void main(String[] args) {
        SwingUtilities.invokeLater(HitwicketGameSwing::new);
    }

    public HitwicketGameSwing() {
        JFrame frame = new JFrame("Hitwicket Game");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setLayout(new BorderLayout());

        // Grid Panel to hold the grid of buttons
        JPanel gridPanel = new JPanel(new GridLayout(BOARD_SIZE, BOARD_SIZE));
        // Control Panel to hold movement buttons
        JPanel controlPanel = new JPanel(new GridLayout(1, 5));
        // Panel for selected button info
        JPanel selectedPanel = new JPanel(new BorderLayout());
        // Label to display the current player
        currentPlayerLabel = new JLabel("Current Player: " + currentPlayer, SwingConstants.CENTER);
        currentPlayerLabel.setForeground(Color.WHITE);
        // Label to display the selected button
        selectedLabel = new JLabel("Selected: None", SwingConstants.CENTER);
        selectedLabel.setForeground(Color.WHITE);

        // Text area to display history of selected buttons
        historyTextArea = new JTextArea(5, 20);
        historyTextArea.setEditable(false);
        historyTextArea.setBackground(Color.BLACK);
        historyTextArea.setForeground(Color.WHITE);
        JScrollPane scrollPane = new JScrollPane(historyTextArea);

        // Background color for the entire frame
        frame.getContentPane().setBackground(Color.BLACK);
        gridPanel.setBackground(Color.BLACK);
        controlPanel.setBackground(Color.BLACK);
        selectedPanel.setBackground(Color.BLACK);

        // Names for Row 1 and Row 5
        String[] row1Names = {"A-P1", "A-P2", "A-H1", "A-H2", "A-P3"};
        String[] row5Names = {"B-P1", "B-P2", "B-H1", "B-H2", "B-P3"};

        // Initialize grid buttons
        for (int i = 0; i < BOARD_SIZE; i++) {
            for (int j = 0; j < BOARD_SIZE; j++) {
                String label = "";

                if (i == 0) { // Row 1 for player A
                    label = row1Names[j];
                } else if (i == BOARD_SIZE - 1) { // Row 5 for player B
                    label = row5Names[j];
                }

                JButton btn = new JButton(label);
                btn.setPreferredSize(new Dimension(60, 60));
                btn.addActionListener(new GridButtonListener());
                btn.setBackground(Color.DARK_GRAY);
                btn.setForeground(Color.WHITE);
                gridButtons[i][j] = btn;
                gridPanel.add(btn);
            }
        }

        // Movement buttons
        JButton moveLeftButton = new JButton("L");
        JButton moveRightButton = new JButton("R");
        JButton moveUpButton = new JButton("F");
        JButton moveDownButton = new JButton("B");

        moveLeftButton.setBackground(Color.DARK_GRAY);
        moveRightButton.setBackground(Color.DARK_GRAY);
        moveUpButton.setBackground(Color.DARK_GRAY);
        moveDownButton.setBackground(Color.DARK_GRAY);

        moveLeftButton.setForeground(Color.WHITE);
        moveRightButton.setForeground(Color.WHITE);
        moveUpButton.setForeground(Color.WHITE);
        moveDownButton.setForeground(Color.WHITE);

        moveLeftButton.addActionListener(e -> handleMoveDirection(-1, 0));
        moveRightButton.addActionListener(e -> handleMoveDirection(1, 0));
        moveUpButton.addActionListener(e -> handleMoveDirection(0, -1));
        moveDownButton.addActionListener(e -> handleMoveDirection(0, 1));

        // Add buttons to the control panel
        controlPanel.add(moveLeftButton);
        controlPanel.add(moveRightButton);
        controlPanel.add(moveUpButton);
        controlPanel.add(moveDownButton);

        // Add selected label to selected panel
        selectedPanel.add(selectedLabel, BorderLayout.SOUTH);
        selectedPanel.add(scrollPane, BorderLayout.CENTER);

        // Layout the frame
        frame.add(currentPlayerLabel, BorderLayout.NORTH);
        frame.add(gridPanel, BorderLayout.CENTER);
        frame.add(controlPanel, BorderLayout.SOUTH);
        frame.add(selectedPanel, BorderLayout.EAST);

        frame.pack();
        frame.setVisible(true);
    }

    private class GridButtonListener implements ActionListener {
        @Override
        public void actionPerformed(ActionEvent e) {
            if (selectedButton != null) {
                selectedButton.setBackground(Color.DARK_GRAY); // Reset previous selection
            }
            selectedButton = (JButton) e.getSource();
            selectedButton.setBackground(Color.BLUE); // Highlight selected button
            selectedLabel.setText("Selected: " + selectedButton.getText());
            historyTextArea.append("Selected: " + selectedButton.getText() + "\n");
        }
    }

    private void handleMoveDirection(int dx, int dy) {
        if (selectedButton == null) {
            System.out.println("No piece selected!");
            return;
        }

        Point selectedPoint = findButtonPosition(selectedButton);
        if (selectedPoint == null) {
            return;
        }

        int newX = selectedPoint.x + dx;
        int newY = selectedPoint.y + dy;

        if (newX >= 0 && newX < BOARD_SIZE && newY >= 0 && newY < BOARD_SIZE) {
            JButton targetButton = gridButtons[newX][newY];

            if (targetButton.getText().isEmpty()) {
                targetButton.setText(selectedButton.getText());
                selectedButton.setText("");
                selectedButton.setBackground(Color.DARK_GRAY);
                selectedButton = null;
                selectedLabel.setText("Selected: None");
                updateGameState();
            } else {
                System.out.println("Invalid move! Target position is occupied.");
            }
        } else {
            System.out.println("Invalid move! Out of bounds.");
        }
    }

    private Point findButtonPosition(JButton button) {
        for (int i = 0; i < BOARD_SIZE; i++) {
            for (int j = 0; j < BOARD_SIZE; j++) {
                if (gridButtons[i][j] == button) {
                    return new Point(i, j);
                }
            }
        }
        return null;
    }

    private void updateGameState() {
        currentPlayer = currentPlayer.equals("A") ? "B" : "A";
        currentPlayerLabel.setText("Current Player: " + currentPlayer);
    }
}
