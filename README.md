# Hospital-Management-System
Login class 

package hospital.management.system;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.sql.ResultSet;

public class Login extends JFrame implements ActionListener {

    JTextField textField;

    JPasswordField jPasswordField;

    JButton b1,b2;

    Login(){

        JLabel namelabel = new JLabel("Username"); // text need to be shown in the window
        namelabel.setBounds(40,30,100,30); // line adjustment in the window
        namelabel.setFont(new Font("Tahoma",Font.BOLD,20));
        namelabel.setForeground(Color.BLACK); // color of the text username
        add(namelabel);

        JLabel password = new JLabel("Password");
        password.setBounds(40,70,100,30);
        password.setFont(new Font("Tahoma",Font.BOLD,20));
        password.setForeground(Color.BLACK); // color of the text username
        add(password);

        textField = new JTextField();
        textField.setBounds(150,30,150,30);
        textField.setFont(new Font("Tahoma",Font.BOLD,15));
        textField.setBackground(new Color(255,255,255));
        add(textField);

        jPasswordField = new JPasswordField();
        jPasswordField.setBounds(150,70,150,30);
        jPasswordField.setFont(new Font("Tahoma",Font.BOLD,15));
        jPasswordField.setBackground(new Color(255,255,255));
        add(jPasswordField);


        //Icon importing
        ImageIcon imageIcon=new ImageIcon((ClassLoader.getSystemResource("icon/login.png")));
        Image i1 = imageIcon.getImage().getScaledInstance(200,200,Image.SCALE_DEFAULT);
        ImageIcon imageIcon1 = new ImageIcon(i1);
        JLabel label =new JLabel(imageIcon1);
        label.setBounds(300,-30,400,300);
        add(label);

        //Buttons
        b1 = new JButton("Login");
        b1.setBounds(165,140,120,30);
        b1.setFont(new Font("serif",Font.BOLD,15));
        b1.addActionListener(this); // Check if the password matches
        add(b1);



        b2 = new JButton("Cancel");
        b2.setBounds(165,180,120,30);
        b2.setFont(new Font("serif",Font.BOLD,15));
        b2.addActionListener(this);
        add(b2);





        getContentPane().setBackground(new Color(109,164,170));//Background color
        setSize(750,300);
        setLocation(400,270);
        setLayout(null);
        setVisible(true);

    }
    // In the class use implement and generate select implement method. This is used for actionlistener
    @Override
    public void actionPerformed(ActionEvent e) {
        if(e.getSource()==b1){
            try{
                conn c = new conn();
                String user = textField.getText();
                String pass = jPasswordField.getText();

                String q = "select * from login where ID = '"+user+"' and PW = '"+pass+"'";
                ResultSet resultSet = c.statement.executeQuery(q);

                if(resultSet.next()){
                    new Reception();
                    setVisible(false);
                }else{
                    JOptionPane.showMessageDialog(null,"Invalid");
                }
                

            }catch(Exception E){
                E.printStackTrace();
            }
        }else {
            System.exit(10);
        }


    }
    public static void main(String[]args){
        new Login();
    }


}
