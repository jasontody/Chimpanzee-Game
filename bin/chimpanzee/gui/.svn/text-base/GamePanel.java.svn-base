package chimpanzee.gui;

import java.awt.Color;
import java.awt.Dimension;
import java.awt.Font;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.TimerTask;

import javax.swing.JButton;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.Timer;


@SuppressWarnings("serial")
public class GamePanel extends JPanel implements ActionListener{

	private BoardPanel board;
	private JButton startGame;
	private CountDownPanel count;
	private CurrentCountPanel current;
	private int stage = 1;
	private RankingPanel ranking;;


	public JLabel lblTime = new JLabel("00:00:00.000");
	private javax.swing.Timer timer;
	private SimpleDateFormat dateFormat, countFormat;
	private Date startDate, endDate;
	public String getTime = "";
	private String rankername;
	private Timer startcount;
	private int countnum ;
	private Boolean failcount=true ;
	RankInfo info = new RankInfo();
	public String usertalk = "";
	
	@Override
	public void actionPerformed(ActionEvent e) {
		// TODO Auto-generated method stub

		if (e.getSource() == timer) {
			if(failcount){
			Date newDate = new Date();
			newDate.setTime(newDate.getTime() - startDate.getTime() + endDate.getTime());
			lblTime.setText(dateFormat.format(newDate));
			}
		}
		if (e.getSource() == startcount){
			Date newDate = new Date();
			newDate.setTime(newDate.getTime() - startDate.getTime() + endDate.getTime());
			if(countnum > 0){
				count.setCount(""+countnum);
				countnum--;
			}
			else if(countnum == 0){
				count.setCount("시작!");
				board.clearAllButtonText();
				countnum--;
			}
		}
		if (e.getSource() == startGame) {
			stage =1;
			startDate = new Date();
			lblTime.setText("00:00:00.000");
			try {
				endDate = dateFormat.parse(lblTime.getText());
			} catch (Exception ex) { }
			timer.start();
			current.setStage(stage);
			playGame();
			startGame.setEnabled(false);
		}
	}

	private BoardListener boardListener = new BoardListener() {

		@Override
		public void Start() {
			// 첫번째 버튼이 눌러졌을 때 호출됨. 게임 시작!
			failcount = true;
			countnum = -1;
			count.setCount("시작!");
			//board.clearAllButtonText();
		}

		@Override
		public void Success() {
			// 모든 버튼을 성공적으로 눌렀을 때 최종적으로 호출됨.
			timer.stop();
			JOptionPane.showMessageDialog(null, "성공하셨습니다. 다음 단계로 넘어갑니다");
			stage++;
			count.setCount("준비!");
			current.setStage(stage);
			playGame();
			InitComponents();
			timer.start();
		}

		@Override
		public void Failure() {
			// 잘못된 버튼을 눌렀을 때 호출됨.
			// 성공했을때와 실패했을때 이루어져야 할 로직이 반대여서 수정하였습니다
			// 성공하면 스테이지를 1 올리고 게임이 계속 되며 실패하면 랭킹에 등록되고 정지됩니다
			
			// 타이머가 살아있으면 종료!
			countnum = -1;
			count.setCount("준비!");
			failcount = false ;
			//timer.stop();
			getTime = lblTime.getText();
			
			JOptionPane.showMessageDialog(null, "게임에 실패했습니다. 다시도전하세요");
			openDialog();
			
			if(rankername != null)			{
				Node userdata = new Node(null, null, stage, rankername , getTime, getTime, usertalk);			
				check(userdata);
			}
			startGame.setEnabled(true);
			lblTime.setText("00:00:00.000");
			GUImain.refresh();
		}
	};

	public void check(Node rank){
		
		Node temp = new Node();
		
		if(info.size==0){
			info.header.setNext(rank);
			rank.setprev(info.header);
			rank.setNext(info.tailer);
			info.tailer.setprev(rank);
			info.size++;
			ranking.RankingAddList(info);
		}
		
		else{
			temp = info.header.getNext(); 
			while(temp!=info.tailer){
				if(rank.get_stage()>temp.get_stage()){
					temp.getBefore().setNext(rank);
					rank.setprev(temp.getBefore());
					temp.setprev(rank);
					rank.setNext(temp);
					info.size++;
					ranking.RankingAddList(info);
					temp = temp.getNext();
					break;
				}
				else if(rank.get_stage()==temp.get_stage()){
					//시간 비교
					int rankmin = Integer.parseInt(rank.get_min().substring(3, 5));
					int tempmin = Integer.parseInt(temp.get_min().substring(3, 5));
					Double ranksec = Double.parseDouble(rank.get_second().substring(6, 12));
					Double tempsec = Double.parseDouble(temp.get_second().substring(6, 12));
					Double ranktime = rankmin*60 + ranksec;
					Double temptime = tempmin*60 + tempsec;
					if(ranktime >temptime){
						temp.getNext().setprev(rank);
						rank.setNext(temp.getNext());
						temp.setNext(rank);
						rank.setprev(temp);
						ranking.RankingAddList(info);
						temp = temp.getNext();
						break;
					}
					else{
						temp.getNext().setprev(rank);
						rank.setNext(temp.getNext());
						temp.setNext(rank);
						rank.setprev(temp);
						ranking.RankingAddList(info);
						temp = temp.getNext();
						break;
					}
				}	
				else{
					if(temp.getNext()==info.tailer){
						temp.getNext().setprev(rank);
						rank.setNext(temp.getNext());
						temp.setNext(rank);
						rank.setprev(temp);
						ranking.RankingAddList(info);
						temp = temp.getNext();
						break;
					}
					else{
						temp = temp.getNext();
					}
				}
				
			}
		}
	}


	public GamePanel(RankingPanel Ranking){
		ranking = Ranking;
		dateFormat = new SimpleDateFormat("HH:mm:ss.SSS");

		count = new CountDownPanel();
		count.setPreferredSize(new Dimension(450, 30));

		board = new BoardPanel();
		board.setPreferredSize(new Dimension(450, 450));
		board.setBoardListener(boardListener);

		current = new CurrentCountPanel();
		current.setPreferredSize(new Dimension(450,35));

		lblTime = new JLabel("00:00:00.000");
		
		
		startGame = new JButton("게임 시작");
		startGame.setFont(new Font("", Font.PLAIN, 30) );
		startGame.setBackground(new Color(40,89,109));
		startGame.setForeground(new Color(54,151,192));
		startGame.setPreferredSize(new Dimension(200, 80) );
		
		
		//restart = new JButton("다시 하기");

		startGame.addActionListener(this);
		//restart.addActionListener(this);

		this.add(count);
		this.add(board);
		this.add(lblTime);
		this.add(current);
		this.add(startGame);	

		InitComponents(); //이부분 위치에 따라서 스탑워치 위치가 바뀜

	}
	private void InitComponents() {
		lblTime.setText("00:00:00.000");
		timer = new javax.swing.Timer(50, this);
	}

	public void openDialog(){
		rankername = JOptionPane.showInputDialog("이름을 입력해 주십시오 (3글자)");
		try{
			while(rankername.length()!=3){	
				rankername = JOptionPane.showInputDialog("3글자로 입력해 주세요");
			}
		}
		catch(Exception e){
		}
		usertalk = JOptionPane.showInputDialog("한마디(10자이내)");
		try{
			while(usertalk.length()>10){
				usertalk = JOptionPane.showInputDialog("10글자 잉내로 입력해주세요");
			}
		}
		catch(Exception e){
		}

	}

	public void playGame(){

		failcount = true ;
		board.clear();
		board.randomGenerate(stage);
		startcount = new Timer(700,this);
		startcount.start();
		countnum = 3;
		countFormat = new SimpleDateFormat("ss");
		GUImain.refresh();
	}

}




