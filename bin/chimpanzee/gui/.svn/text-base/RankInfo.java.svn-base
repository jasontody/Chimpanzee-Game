package chimpanzee.gui;

public class RankInfo{
	Node header;
	Node tailer;
	int size;
	public RankInfo()
	{
		header = new Node(null, null, 0, "" , "", "", "");
		tailer = new Node(null, header, 0, "", "", "", "");
		header.setNext(tailer);
		size = 0;
	}
}
class Node
{
	Node next;
	Node before;
	private String name;
	private int stage;
	private String miniute;
	private String second;
	private String talk;
	
	public Node(){
		this(null,null,0," "," "," "," ");
	}
	
	public Node(Node next,Node before,int stage,String name,String minute,String second,String usertalk){

		this.next = next;
		this.stage=stage;
		this.before = before;
		this.name = name;
		this.miniute = minute;
		this.second = second;
		this.talk = usertalk;
	}
	public String get_min(){
		return miniute;
	}
	public String get_second()
	{
		return second;
	}
	public String get_name(){
		return name;
	}
	public  int get_stage(){
		return stage;
	}	
	public String get_talk(){
		return talk;
	}
	public Node getNext(){
		return next;
	}
	public Node getBefore(){
		return before;
	}
	public void setNext(Node n){
		next = n;
	}
	public void setprev(Node p){
		before = p;
	}
}




