import javax.swing.*;

import java.awt.*;

import java.awt.event.*;

import java.util.ArrayList;

import java.util.Random;

public class SnakeGame extends JFrame {

 public SnakeGame() {

 this.add(new GamePanel());

 this.setTitle("Snake Game");

 this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

 this.setResizable(false);

 this.pack();

 this.setLocationRelativeTo(null);

 this.setVisible(true);

 }

 public static void main(String[] args) {

 new SnakeGame();

 }

}

class GamePanel extends JPanel implements ActionListener {

 private final int TILE_SIZE = 25; // Size of each tile

 private final int GAME_WIDTH = 500;

 private final int GAME_HEIGHT = 500;

private final int TOTAL_TILES = (GAME_WIDTH * GAME_HEIGHT) / 

(TILE_SIZE * TILE_SIZE);

 private final int[] x = new int[TOTAL_TILES];

 private final int[] y = new int[TOTAL_TILES];

 private int bodyParts = 3; // Initial snake size

 private int foodX, foodY; // Food position

 private int score = 0;

 private char direction = 'R'; // Initial direction: R = right

 private boolean running = false;

 private Timer timer;

 private Random random;

 public GamePanel() {this.setPreferredSize(new Dimension(GAME_WIDTH, GAME_HEIGHT));

 this.setBackground(Color.BLACK);

 this.setFocusable(true);

 this.addKeyListener(new MyKeyAdapter());

 random = new Random();

 startGame();

 }

 private void startGame() {

 spawnFood();

 running = true;

 timer = new Timer(100, this); // Speed of the game

 timer.start();

 }

 private void spawnFood() {

 foodX = random.nextInt(GAME_WIDTH / TILE_SIZE) * TILE_SIZE;

 foodY = random.nextInt(GAME_HEIGHT / TILE_SIZE) * TILE_SIZE;

 }

 private void move() {

 for (int i = bodyParts; i > 0; i--) {

 x[i] = x[i - 1];

 y[i] = y[i - 1];

 }

 switch (direction) {

 case 'U' -> y[0] -= TILE_SIZE;

 case 'D' -> y[0] += TILE_SIZE;

 case 'L' -> x[0] -= TILE_SIZE;

 case 'R' -> x[0] += TILE_SIZE;

 }

 }

 private void checkFood() {

 if ((x[0] == foodX) && (y[0] == foodY)) {

 bodyParts++;

 score++;

 spawnFood();

 }

 }

 private void checkCollisions() {

 // Check if head collides with body

 for (int i = bodyParts; i > 0; i--) {

 if ((x[0] == x[i]) && (y[0] == y[i])) {

 running = false;

 }

 }

 // Check if head touches walls

 if (x[0] < 0 || x[0] >= GAME_WIDTH || y[0] < 0 || y[0] >= GAME_HEIGHT) {

 running = false;

 }

 if (!running) {

 timer.stop();

 }

 }

 private void gameOver(Graphics g) {

 g.setColor(Color.RED);

 g.setFont(new Font("Arial", Font.BOLD, 40));

 FontMetrics metrics = getFontMetrics(g.getFont());

 g.drawString("Game Over", (GAME_WIDTH - metrics.stringWidth("Game 

Over")) / 2, GAME_HEIGHT / 2);

 g.setColor(Color.WHITE);

 g.setFont(new Font("Arial", Font.PLAIN, 20));

 g.drawString("Score: " + score, (GAME_WIDTH - metrics.stringWidth("Score: " 

+ score)) / 2, GAME_HEIGHT / 2 + 50);

 }

 @Override

 protected void paintComponent(Graphics g) {

 super.paintComponent(g);

 if (running) {

 g.setColor(Color.RED);

 g.fillOval(foodX, foodY, TILE_SIZE, TILE_SIZE);

 for (int i = 0; i < bodyParts; i++) {

 if (i == 0) {

 g.setColor(Color.GREEN);

 } else {

 g.setColor(new Color(45, 180, 0));

 }

 g.fillRect(x[i], y[i], TILE_SIZE, TILE_SIZE);

 }

 g.setColor(Color.WHITE);

 g.setFont(new Font("Arial", Font.PLAIN, 2} else {

 gameOver(g);

 }

 }

 @Override

 public void actionPerformed(ActionEvent e) {

 if (running) {

 move();

 checkFood();

 checkCollisions();

 }

 repaint();

 }

 private class MyKeyAdapter extends KeyAdapter {

 @Override

 public void keyPressed(KeyEvent e) {

 switch (e.getKeyCode()) {

 case KeyEvent.VK_LEFT -> {

 if (direction != 'R') direction = 'L';

 }

 case KeyEvent.VK_RIGHT -> {

 if (direction != 'L') direction = 'R';

 }

 case KeyEvent.VK_UP -> {

 if (direction != 'D') direction = 'U';

 }

 case KeyEvent.VK_DOWN -> {

 if (direction != 'U') direction = 'D';

 }

 }

 }

 }

}
