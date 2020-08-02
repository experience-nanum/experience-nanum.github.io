---
title: "July algorithm1"
category: 
    - Algorithm
tag :
    - stack
toc: true
---


## [문제 URL](https://www.acmicpc.net/problem/10828)


## 풀이
```java
import java.util.ArrayList;
import java.util.List;
import java.util.Objects;
import java.util.Scanner;

public class StackMain {
	private int top;
	private int size;
	private String[] stackArr;
	
	private final int ZERO = 0; 
	private final int MINUS_ONE = -1; 
	private final int ONE = 1; 
	private final String END = "end"; 
	
	StackMain(int size){
		top = MINUS_ONE;
		this.size = size;
		stackArr = new String[this.size];
	}
	
	@SuppressWarnings("resource")
	public static void main(String[] args) {
		StackMain stack = new StackMain(10);
		
		Scanner sc = new Scanner(System.in);
		String command = "";
		CommandType type = CommandType.PUSH;
		
		while (!"end".equals(command)) {
			System.out.print("명령어 입력: "); 
			command = sc.nextLine();
			type = stack.getType(command);
		
			/** command 분기 */
			switch (type) {
			case PUSH:
				stack.push(command);
				break;
			case POP:
				stack.pop(command);
				break;
			case SIZE:
				stack.size(command);
				break;
			case EMPTY:
				stack.empty(command);
				break;
			case TOP:
				stack.top(command);
				break;
			default:
				break;
			}
		}
		//stack.printResult();
	}
	
	/** command 타입 체크 */
	public CommandType getType(String command) {
		CommandType type = CommandType.END;
		for (CommandType com:CommandType.values()) {
			if(command.contains(com.getCommand())) {
				type = com;
				break;
			}
		}
		return type;
	}
	
	/** command 타입 정리 */
	public enum CommandType{
		PUSH("push", 0) 
		,POP("pop", 2) 
		,SIZE("size", 3) 
		,EMPTY("empty",4) 
		,TOP("top", 5)
		,END("end", 6);
		 
		private String command; 
		private Integer commandNum; 
		CommandType(String command, Integer commandNum){
			this.command = command;
			this.commandNum = commandNum;
		}
		
		public String getCommand() { 
			return command; 
		}
		public Integer getCommandNum() { 
			return commandNum; 
		}
	}
	
	/** command 수행 */
	public void push(String command) {
		String push = CommandType.PUSH.getCommand();
		command = command.replace(push, "").trim();
		if(top != this.size && !"".equals(command))
			stackArr[++top]= command;
	}
	public void pop(String command) {
		if(empty()) {
			System.out.println(MINUS_ONE);
		}else {
			System.out.println(stackArr[top--]);
		}
	}
	public void size(String command) {
		if(empty()) {
			System.out.println(top);
		}else {
			System.out.println(top+1);
		}
	}
	public void empty(String command) { //호출용
		if(top == MINUS_ONE) {
			System.out.println(ONE);
		}else {
			System.out.println(ZERO);
		}
	}
	public boolean empty() { //empty 체크용
		return (top == MINUS_ONE);
	}
	public void top(String command) {
		if(empty()) {
			System.out.println(MINUS_ONE);
		}else {
			System.out.println(stackArr[top]);
		}
	}
	public void printResult() {
		for(int i=0; i<=top; i++) {
			System.out.println(stackArr[i]);
		}
	}

}

```