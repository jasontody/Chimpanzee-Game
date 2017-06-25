package chimpanzee.gui;

import java.awt.Color;
import java.awt.Dimension;
import java.awt.Font;

import javax.swing.JLabel;
import javax.swing.JPanel;

@SuppressWarnings("serial")
public class CurrentCountPanel extends JPanel {
	
	private JLabel stage = new JLabel("STAGE 1");
	
	public CurrentCountPanel(){

		stage.setFont(new Font("굴림",Font.PLAIN, 20));
		stage.setFont(new Font("굴림",Font.BOLD, 20));
		stage.setSize(50,20);
		this.add(stage);

	}
	
	public void setStage(int num){
		this.stage.setText("STAGE "+num);
		this.stage.setForeground(new Color(54,151,192));
		GUImain.refresh();
	}

}
