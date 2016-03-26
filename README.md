# Calculadora-Modificada-Exercicio-4
Exercicio 4 CES-22

import javax.swing.*;     // Para os Frames
import java.awt.*;        // Para a interface grafica
import java.awt.event.*;  // Para os eventos
import java.util.ArrayList;
import java.awt.Font;

public class Calculadora extends JFrame implements ActionListener{

	private JPanel Panel = new JPanel ();
	private TextArea Screen = new TextArea(1, 100);
	
	private JButton botao1, botao2, botao3, botao4, botao5, botao6, botao7, botao8, botao9, botao_Adicao, botao_Subt, botao_Mult, botao_Div, botao_Igual;
	private JButton botao_Limpar, botao0;
	
	private int value, armazenado;
	private String Operacao;
	
	public Calculadora ()
	{
		Screen.setEditable(false);
		
		botao0 = new JButton ("0");
		botao1 = new JButton ("1");
		botao2 = new JButton ("2");
		botao3 = new JButton ("3");
		botao4 = new JButton ("4");
		botao5 = new JButton ("5");
		botao6 = new JButton ("6");
		botao7 = new JButton ("7");
		botao8 = new JButton ("8");
		botao9 = new JButton ("9");
		botao_Adicao = new JButton ("+");
		botao_Subt = new JButton("-");
		botao_Mult = new JButton("*");
		botao_Div = new JButton("/");
		botao_Igual = new JButton("=");
		
		botao_Limpar = new JButton("Clear");
		
		Panel.add(botao0);
		Panel.add(botao1);
		Panel.add(botao2);
		Panel.add(botao3);
		Panel.add(botao4);
		Panel.add(botao5);
		Panel.add(botao6);
		Panel.add(botao7);
		Panel.add(botao8);
		Panel.add(botao9);
		Panel.add(botao_Adicao);
		Panel.add(botao_Subt);
		Panel.add(botao_Mult);
		Panel.add(botao_Div);
		Panel.add(botao_Igual);
		Panel.add(botao_Limpar);
		
		botao0.addActionListener(this);
		botao1.addActionListener(this);
		botao2.addActionListener(this);
		botao3.addActionListener(this);
		botao4.addActionListener(this);
		botao5.addActionListener(this);
		botao6.addActionListener(this);
		botao7.addActionListener(this);
		botao8.addActionListener(this);
		botao9.addActionListener(this);
		
		botao_Adicao.addActionListener(this);
		botao_Subt.addActionListener(this);
		botao_Mult.addActionListener(this);
		botao_Div.addActionListener(this);
		botao_Igual.addActionListener(this);
		botao_Limpar.addActionListener(this);
		
		
		Panel.add(Screen);
		
		this.add(Panel);
		
		value = 0;
		armazenado = 0;
	}
	
	public void actionPerformed (ActionEvent e)
	{
		Object source = e.getSource();
		if (source == botao0)
			Screen.append("0");
		else if (source == botao1)
		{
			value = value*10 + 1;	
			Screen.append("1");
		}
		else if (source == botao2)
		{
			value = value*10 + 2;	
			Screen.append("2");
		}
		else if (source == botao3)
		{
			value = value*10 + 3;	
			Screen.append("3");
		}
		else if (source == botao4)
		{
			value = value*10 + 4;	
			Screen.append("4");
		}
		else if (source == botao5)
		{
			value = value*10 + 5;	
			Screen.append("5");
		}
		else if (source == botao6)
		{
			value = value*10 + 6;	
			Screen.append("6");
		}
		else if (source == botao7)
		{
			value = value*10 + 7;	
			Screen.append("7");
		}
		else if (source == botao8)
		{
			value = value*10 + 8;	
			Screen.append("8");
		}
		else if (source == botao9)
		{
			value = value*10 + 9;	
			Screen.append("9");
		}
		else if (source == botao_Adicao)
		{
			Operacao = "+";
			armazenado = value;
			value = 0;
			Screen.setText("Operacao Soma. Digite o proximo numero: ");
		}
		else if (source == botao_Subt)
		{
			Screen.setText("Operacao Subtracao. Digite o proximo numero: ");
			Operacao = "-";
			armazenado = value;
			value = 0;
		}
		else if (source == botao_Mult)
		{
			Screen.setText("Operacao Mult. Digite o proximo numero: ");
			Operacao = "*";
			armazenado = value;
			value = 0;
		}
		else if (source == botao_Div)
		{
			Screen.setText("Operacao Div. Digite o proximo numero: ");
			Operacao = "/";
			armazenado = value;
			value = 0;
		}
		else if (source == botao_Igual)
		{
			try
			{
				compute();
			}
			catch (Divide_by_Zero_Exception e1)
			{    
				Screen.setText("Erro: Divisao por Zero!");;
			}
		}
		else if (source == botao_Limpar)
		{
			value = 0;
			armazenado = 0;
			Screen.setText("");
		}
	}
	
	void compute () throws Divide_by_Zero_Exception 
	{
		if (Operacao == "+")
		{
			value = value + armazenado;
			Screen.setText("" + value + "");
		}
		else if (Operacao == "-")
		{
			value = armazenado - value;
			Screen.setText("" + value + "");
		}
		else if (Operacao == "*")
		{
			value = value * armazenado;
			Screen.setText("" + value + "");
		}
		else if (Operacao == "/")
		{
			if (value == 0)
			{  
			   throw new Divide_by_Zero_Exception();
			}
			else { value = armazenado / value; Screen.setText("" + value + ""); }
		}
	}
	
	public static void main(String[] args) {
		
		Calculadora Calc = new Calculadora ();
		
		Calc.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
	
		Calc.pack();
		Calc.setVisible(true);
		
	}
}
