# Cách mở dialog trong java swing ide netbean

rong các ứng dụng Desktop chắc hẳn nhu cầu hiển thị một hộp thoại để thông báo cho người dùng một thông tin gì đó hay để xác nhận lại một hành động là một điều thiết yếu. 

Để làm được điều này, Java Swing đã hỗ trợ cho chúng ta một thành phần đó là JOptionPane, JDialog cho phép chúng ta tạo ra các hộp thoại với các mục đích khác nhau.

##  JOptionPane

JOptionPane cho phép chúng ta nhanh chóng tạo ra các hộp thoại với các văn bản, icon, tiêu đề khác nhau.

JOptionPane hỗ trợ 4 loại Icon cho các hộp thoại dạng câu hỏi, thông tin, cảnh báo và lỗi.

Cách sử dụng JOptionPane khá đơn giản chúng ta chỉ cần xác định JFrame chính mà nó thuộc về, tin nhắn hiện thị đến người dùng và loại Icon tương ứng. Sau đó gọi hàm **showMessageDialog**.

### Information Dialog

```
import javax.swing.*;

public class Main {
    public static void main(String[] args) {

        // create a jframe
        JFrame frame = new JFrame("JOptionPane showMessageDialog example");

        JOptionPane.showMessageDialog(frame,
                "Message Example",
                "Title Example",
                JOptionPane.INFORMATION_MESSAGE);
    }
}
```

![image](https://github.com/thangdtph27626/dialogInJavaSwing/assets/109157942/13ca8d70-7434-4036-8a7e-9eb0b1fae61d)

### Error Dialog

Tương tự nếu các bạn muốn thông báo một lỗi đến người dùng thì có thể điều chỉnh tin nhắn và Icon Error.

```
import javax.swing.*;

public class Main {
    public static void main(String[] args) {

        // create a jframe
        JFrame frame = new JFrame("JOptionPane showMessageDialog example");

        JOptionPane.showMessageDialog(frame,
                "Error Message",
                "Error Title",
                JOptionPane.ERROR_MESSAGE);
    }
}
```

![image](https://github.com/thangdtph27626/dialogInJavaSwing/assets/109157942/7e5aec74-a347-4956-8c13-582f8654d6ec)

### Yes – No Dialog

Trong trường hợp bạn muốn người dùng xác nhận lại hành động họ vừa mới thực hiện thì chúng ta có thể dùng Yes No Dialog cho phép người dùng xác nhận lại. Nếu họ chọn Yes hành động trước đó sẽ được thực hiện, ngược lại thì không.

Ví tạo tạo một ứng dụng gồm có Button “Lưu”, khi nhấn vào nút này thì sẽ hiện lên hộp thoại hỏi người dùng xác nhận có lưu hay không?

```
package com.company;

import java.awt.BorderLayout;
import java.awt.FlowLayout;
import java.awt.LayoutManager;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;

public class Main {
    public static void main(String[] args) {
        createWindow();
    }

    private static void createWindow() {
        JFrame frame = new JFrame("Swing Tester");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        createUI(frame);
        frame.setSize(560, 200);
        frame.setLocationRelativeTo(null);
        frame.setVisible(true);
    }

    private static void createUI(final JFrame frame){
        JPanel panel = new JPanel();
        LayoutManager layout = new FlowLayout();
        panel.setLayout(layout);

        JButton button = new JButton("Lưu sinh viên");
        final JLabel label = new JLabel();
        button.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                int result = JOptionPane.showConfirmDialog(frame,
                        "Bạn có chắc muốn lưu sinh viên này",
                        "Xác nhận",
                        JOptionPane.YES_NO_OPTION,
                        JOptionPane.QUESTION_MESSAGE);
                if(result == JOptionPane.YES_OPTION){
                    label.setText("Bạn chọn: Yes");
                }else if (result == JOptionPane.NO_OPTION){
                    label.setText("Bạn chọn : No");
                }else {
                    label.setText("Chưa ");
                }
            }
        });

        panel.add(button);
        panel.add(label);
        frame.getContentPane().add(panel, BorderLayout.CENTER);
    }
} 
```

![image](https://github.com/thangdtph27626/dialogInJavaSwing/assets/109157942/71d1ce3b-fbee-412c-bb0a-e8839c1439ce)

### Yes – No – Cancel Dialog

Ngoài ra chúng ta có thể tạo hộp thoại với cả 3 lựa chọn Yes, No và Cancel với **JOptionPane.YES_NO_CANCEL_OPTION**.

```
package com.company;

import java.awt.BorderLayout;
import java.awt.FlowLayout;
import java.awt.LayoutManager;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;

public class Main {
    public static void main(String[] args) {
        createWindow();
    }

    private static void createWindow() {
        JFrame frame = new JFrame("Swing Tester");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        createUI(frame);
        frame.setSize(560, 200);
        frame.setLocationRelativeTo(null);
        frame.setVisible(true);
    }

    private static void createUI(final JFrame frame){
        JPanel panel = new JPanel();
        LayoutManager layout = new FlowLayout();
        panel.setLayout(layout);

        JButton button = new JButton("Lưu sinh viên");
        final JLabel label = new JLabel();
        button.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                Object[] options = {"Có, chắc rồi", "Không, tôi đã thay đổi ý định", "Thôi bỏ"};
                int result = JOptionPane.showOptionDialog(frame,
                        "Bạn có chắc muốn lưu sinh viên này",
                        "Xác nhận",
                        JOptionPane.YES_NO_CANCEL_OPTION,
                        JOptionPane.QUESTION_MESSAGE,
                        null,
                        options,
                        options[0]);
                if(result == JOptionPane.YES_OPTION){
                    label.setText("Bạn chọn: Yes");
                }else if (result == JOptionPane.NO_OPTION){
                    label.setText("Bạn chọn : No");
                } else if (result == JOptionPane.CANCEL_OPTION) {
                    label.setText("Ban chon cancel");
                }else {
                    label.setText("Chưa ");
                }
            }
        });

        panel.add(button);
        panel.add(label);
        frame.getContentPane().add(panel, BorderLayout.CENTER);
    }
} 
```

![image](https://github.com/thangdtph27626/dialogInJavaSwing/assets/109157942/c04ce4c7-9a71-4038-90c0-a23cf741811e)

Như vậy chúng ta có thể thấy rằng cả 3 hàm showMessageDialog, showConfirmDialog và showOptionDialog đều trả về một số nguyên cho biết sự lựa chọn của người dùng. Các giá trị số nguyên này được chỉ định bởi các hằng số YES_OPTION, NO_OPTION, CANCEL_OPTION, OK_OPTION, CLOSED_OPTION.

### JDialog

Trong khi JOptionPane là cung cấp các method được xây dựng sẵn hỗ trợ cho chúng ta có thể nhanh chóng tạo ra các hộp thoại một cách nhanh chóng.

Thế nhưng các hộp thoại được tạo ra bởi JOptionPane tương đối đơn giản và sẽ không thể đáp ứng đủ nếu nhu cầu của bạn muốn có một hộp loại phức tạp hơn.

Đây chính là lúc chúng ta cần dùng đến JDialog, nó cho phép chúng ta tạo ra một layout với các thành phần con do chúng ta tự định nghĩa và xử lý các sự kiện cho chúng. Do vậy một JDialog có thể đáp ứng hầu hết các nhu cầu khó nhằn nhất của các bạn.

Trong phần này mình sẽ lấy ví dụ tạo ra một hộp thoại với một Label và Button khi nhấp vào sẽ tự động đóng hộp thoại. 

```
package com.company;

import javax.swing.*;
import javax.swing.border.EmptyBorder;
import java.awt.*;

public class DialogExample {
    public static void main(String[] args) {
        JFrame frame = new JFrame();
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(400, 400);

        JDialog dialog = new JDialog(frame, "Dialog", true);

        JPanel mainGui = new JPanel(new BorderLayout());
        mainGui.setBorder(new EmptyBorder(20, 20, 20, 20));
        mainGui.add(new JLabel("Đóng hộp thoại"), BorderLayout.CENTER);

        JPanel buttonPanel = new JPanel(new FlowLayout());
        mainGui.add(buttonPanel, BorderLayout.SOUTH);

        JButton close = new JButton("Đóng");
        close.addActionListener(e->dialog.setVisible(false));

        buttonPanel.add(close);

        frame.setVisible(true);

        dialog.setContentPane(mainGui);
        dialog.pack();
        dialog.setVisible(true);
    }
} 
```

![image](https://github.com/thangdtph27626/dialogInJavaSwing/assets/109157942/70d8a72a-b4d3-48cf-999a-098cf9f29df8)
