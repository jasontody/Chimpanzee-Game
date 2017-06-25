package chimpanzee.gui;

import javax.swing.JFrame;
import javax.swing.JTabbedPane;

public class GUImain {
	
	private static JFrame frame;
	private JTabbedPane mainPane;
	private GamePanel game;
	public RankingPanel ranking; 
	
	public GUImain(){
		ranking = new RankingPanel();
		game = new GamePanel(ranking);
		
		mainPane = new JTabbedPane();
		mainPane.addTab("게임 하기", game);
		mainPane.addTab("랭킹 확인하기", ranking);
		
		frame = new JFrame();
		frame.setTitle("CHIMPANZEE-GAME!!");
		frame.setSize(500, 720);
		frame.setResizable(false);
		frame.setContentPane(mainPane);
		frame.setVisible(true);
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		
	}
	
	public static void main(String[] args) {
		new GUImain();
	}
	
	public static void refresh(){
		frame.repaint();
	}

}
