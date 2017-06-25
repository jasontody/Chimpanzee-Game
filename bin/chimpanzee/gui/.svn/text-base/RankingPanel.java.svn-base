package chimpanzee.gui;

import java.awt.Color;
import java.awt.Dimension;
import java.awt.Font;

import javax.sound.sampled.Line;
import javax.swing.DefaultListModel;
import javax.swing.JLabel;
import javax.swing.JList;
import javax.swing.JPanel;
import javax.swing.border.LineBorder;

@SuppressWarnings("serial")



public class RankingPanel extends JPanel{
	
	private DefaultListModel model = new DefaultListModel();
	private JList list = new JList(model);
	private String getTime ;
	private JLabel rankingtitle;
	private String rankingname;
	
	public RankingPanel(){
		rankingtitle = new JLabel("<랭킹>");
		rankingtitle.setFont(new Font("굴림",Font.PLAIN, 20));
		rankingtitle.setFont(new Font("굴림",Font.BOLD, 20));
		rankingtitle.setForeground(new Color(20,107,110));
		rankingtitle.setSize(50,30);
		list.setBorder(new LineBorder(new Color(20,107,110), 2));
		this.add(rankingtitle);
		
		addToList("                                랭킹 정보가 없습니다. 게임을 플레이 해 주세요");
		addToList(getTime);
		list.setPreferredSize(new Dimension(450, 600));
		
		this.add(list);
	}
	
	public void RankingAddList(RankInfo info){
		String data = "";
		Node temp = new Node();
		temp = info.header.getNext();
		clearedList();
		rankingname = "    랭킹      이름       스테이지           시간                         한마디:)";
		list.setForeground(new Color(0,0,0));
		
		this.addToList(rankingname);
		int i=1;
		while(temp!=info.tailer){
			data = data+"      "+ i + "       "+temp.get_name() + "           " + temp.get_stage() + 
			"             " + temp.get_min() + "          " + temp.get_talk() ;
			this.addToList(data);
			data = "";
			temp = temp.getNext();	
			i++;
		}
	}
	
	
	public void addToList(Object object){
		model.addElement(object);
	}
	public void clearedList(){
		model.clear();
	}

	public DefaultListModel getModel(){
		return model;
	}

}
