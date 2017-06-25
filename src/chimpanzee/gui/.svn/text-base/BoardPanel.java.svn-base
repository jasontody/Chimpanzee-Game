package chimpanzee.gui;

import java.awt.Color;
import java.awt.Dimension;
import java.awt.Font;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.Calendar;
import java.util.Iterator;
import java.util.LinkedList;
import java.util.Queue;
import java.util.Random;

import javax.swing.JButton;
import javax.swing.JPanel;


interface BoardListener {
	public void Start();
	public void Success();
	public void Failure();
}

@SuppressWarnings("serial")
public class BoardPanel extends JPanel {

	private BoardListener listener;
	
	private Queue<JButton> queue;
	private int gridRows = 6;
	private int gridCols = 6;
	
	private int totalCount;
	
	public void setBoardListener( BoardListener listener )	{
		this.listener = listener;
	}
	
	private ActionListener action = new ActionListener() {
		@Override
		public void actionPerformed(ActionEvent e) {
			// 큐에다가 버튼을 넣고
			// 여기서 눌려진 버튼이 top(peek)이면 그 버튼을 부모로부터 제거하고
			// 큐에서 pop(poll) 한다.
			// 큐가 다 비워지면 완료 메세지를 출력한다.
			
			if( false == queue.isEmpty() ){
				JButton btn = (JButton)e.getSource();
				if( btn.equals(queue.peek()))	{
					// 첫 버튼을 정상적으로 눌렀을때만 다른버튼을 모두 가림.
					if(totalCount == queue.size()){
						// 게임 시작~!
						if(listener != null)
							listener.Start();
						clearAllButtonText();
					}

					// 부모로부터 버튼을 떼어버림.
					JPanel p = (JPanel)btn.getParent();
					p.removeAll();
					p.repaint();
		
					// 큐에서 제거.
					queue.poll();
				}
				else				{
					disableAllButton();
					// 잘못된 버튼을 눌러서 게임 실패!
					if(listener != null)
						listener.Failure();
				}		
			}
			if( queue.isEmpty()){
				// 다 눌러서 성공!
				if(listener != null)
					listener.Success();
			}
		}
	};
	
	public BoardPanel(){
		queue = new LinkedList<JButton>();
		clear();
	}
	
	public void clear(){
		this.removeAll();
		
		GridLayout grid = new GridLayout(gridRows, gridCols);
		this.setLayout(grid);
		for (int i = 0; i < gridRows*gridCols; i++) {
			JPanel blank = new JPanel();
			blank.setBackground(Color.black);
			this.add(blank);
		}
		queue.clear();
	}
	
	private JPanel getRandomBlankPanel()	{
		JPanel randomPanel;
		while(true)		{
			// 랜덤 인덱스를 구해서 그 Panel이 비어있으면 리턴함.(있으면 다시 랜덤)
			int randomIndex = (int)(Math.random() * (gridRows*gridCols));
			randomPanel = (JPanel)this.getComponent(randomIndex);
			if(randomPanel.getComponentCount() == 0)
				break;
		}
		return randomPanel;
	}
	
	public void randomGenerate(int number){
		
		// 빈칸보다 버튼을 많이 만들려고 하면 그냥 리턴.
		if(number > gridRows*gridCols)
			return;
		
		totalCount = number;
		
		for (int i = 0; i < number; i++) {
			JButton tempButton = new JButton(i+1+"");
			tempButton.setForeground(new Color(255,38,6));
			tempButton.setPreferredSize(new Dimension(super.getWidth()/gridRows, super.getHeight()/gridCols));
			tempButton.addActionListener(action);
			tempButton.setFocusable(false);
			tempButton.setFont( new Font( "",Font.BOLD, 30 ) );
			JPanel randomPanel = getRandomBlankPanel();
			randomPanel.add(tempButton);
			queue.offer(tempButton);			
		}
	}
	
	
	public void clearAllButtonText(){
		Iterator<JButton> iter = queue.iterator();
		while( iter.hasNext() ) {
			JButton btn = iter.next();
			btn.setText("");
		}
	}
	
	public void disableAllButton(){
		// 모든 버튼을 disable 시킴.
		Iterator<JButton> iter = queue.iterator();
		while( iter.hasNext() ) {
			JButton btn = iter.next();
			btn.setEnabled(false);
		}
		
		// 다시 버튼들의 번호를 출력함.
		int i = totalCount - queue.size();
		iter = queue.iterator();
		while( iter.hasNext() ) {
			JButton btn = iter.next();
			btn.setText(i+1+"");
			i++;
		}

	}
}
