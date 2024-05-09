using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Net.Sockets;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using Modbus.Device; //네임스페이스 추가하기

namespace _20240307
{
    public partial class Form1 : Form
    {
        TcpClient tc = new TcpClient();
        ModbusIpMaster mim;

        Label[] mylabel = new Label[16];
        public Form1()
        {
            InitializeComponent();
            mylabel[0] = label4; //공급후진
            mylabel[1] = label3; //공급전진
            mylabel[2] = label1; //자재투입감지
            mylabel[3] = label5;
            mylabel[4] = label6;
            mylabel[5] = label7;
            mylabel[6] = label8;
            mylabel[7] = label9;
            mylabel[8] = label10;
            mylabel[9] = label12;
            mylabel[10] = label11;
            mylabel[11] = label14;
            mylabel[12] = label13;
            mylabel[13] = label15;
            mylabel[14] = label16;
            mylabel[15] = label17;

        }

        private void button1_Click(object sender, EventArgs e)
        {
            //장비와 Tcp 연결하기
            tc.Connect(textBox1.Text, 502);
            mim = ModbusIpMaster.CreateIp(tc);

            mim.Transport.ReadTimeout = 100;
            mim.Transport.WriteTimeout = 100;
            mim.Transport.Retries = 0;

            if(tc.Connected)
            {
                timer1.Start();
                MessageBox.Show("접속");
            }
        }

        private void button2_Click(object sender, EventArgs e)
        {
            //실린더전진
            try
            {
                mim.WriteSingleCoil(0, true);
            }
            catch
            {
                MessageBox.Show("실패");
            }
           

        }

        private void button3_Click(object sender, EventArgs e)
        {
            try
            {
                mim.WriteSingleCoil(0, false);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void button4_Click(object sender, EventArgs e)
        {
           
            try
            {
                /*
                //읽기코일 0번지부터 3개의 버튼을 읽어오겠다
                bool[] datat = mim.ReadInputs(0, 3);
                if (datat[0])
                {
                    //공급후진감지 센서가 작동중
                    label4.Text = "실린더후진센서 : 감지";
                }
                else
                {
                    //감지 안된상태
                    label4.Text = "실린더후진센서 : 미감지";
                }
                if (datat[1])
                {
                    //실린더가 전진센서에 감지됨
                    label3.Text = "실린더전진센서 : 감지";
                }
                else
                {
                    //감지안됨
                    label3.Text = "실린더전진센서 : 미감지";

                }
                if (datat[2])
                {
                    //실린더가 전진센서에 감지됨
                    label1.Text = "자재감지센서 : 감지";
                }
                else
                {
                    //감지안됨
                    label1.Text = "자재감지센서 : 미감지";

                }

                /*
                bool[] data = mim.ReadCoils(0, 1);
                if (data[0])
                {
                    //실린더가 전진해있는 상태
                    label1.Text = "결과 : 전진";
                }
                else
                {
                    //후진해있는 상태
                    label1.Text = "결과 : 후진";
                }
                */
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void button5_Click(object sender, EventArgs e)
        {
            try
            {
                mim.WriteSingleCoil(1, true);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void button6_Click(object sender, EventArgs e)
        {
            try
            {
                mim.WriteSingleCoil(1, false);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void button7_Click(object sender, EventArgs e)
        {
            try
            {
                                         //쓰기코일 1번을 시작주소로 해서 1개
                bool[] data = mim.ReadCoils(1, 1);
                if (data[0])
                {
                    //실린더가 전진해있는 상태
                    label2.Text = "결과 : 작동 중";
                }
                else
                {
                    //후진해있는 상태
                    label2.Text = "결과 : 멈춤";
                }
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void timer1_Tick(object sender, EventArgs e)
        {
           
            //타이머가 작동주이라면 뭐할래?
            try
            {
                bool[] data = mim.ReadInputs(0, 16);
                for (int i =0; i<16; i++)
                {
                    if (data[i])
                    {
                        mylabel[i].BackColor = Color.Green;
                    }
                    else
                    {
                        mylabel[i].BackColor = Color.Red;
                    }
                }

               

                /*
                //읽기코일 0번지부터 3개의 버튼을 읽어오겠다
                if (datat[0])
                {
                    //공급후진감지 센서가 작동중
                    // label4.Text = "실린더후진센서 : 감지";
                    label4.BackColor = Color.Green;
                }
                else
                {
                    //감지 안된상태
                    //label4.Text = "실린더후진센서 : 미감지";
                    label4.BackColor = Color.Red;
                }
                if (datat[1])
                {
                    //실린더가 전진센서에 감지됨
                    //label3.Text = "실린더전진센서 : 감지";
                    label3.BackColor = Color.Green;
                }
                else
                {
                    //감지안됨
                    //label3.Text = "실린더전진센서 : 미감지";
                    label3.BackColor = Color.Red;

                }

                if (datat[2])
                {
                    //실린더가 전진센서에 감지됨
                    //label1.Text = "자재감지센서 : 감지";
                    label1.BackColor = Color.Green;
                }
                else
                {
                    //감지안됨
                    //label1.Text = "자재감지센서 : 미감지";
                    label1.BackColor = Color.Red;

                }

                if (datat[3])
                {
                    //실린더가 전진센서에 감지됨
                    label5.BackColor = Color.Green;
                }
                else
                {
                    //감지안됨
                    label5.BackColor = Color.Red;

                }

                if (datat[4])
                {
                    //실린더가 전진센서에 감지됨
                    label6.BackColor = Color.Green;
                }
                else
                {
                    //감지안됨
                    label6.BackColor = Color.Red;

                }


                /*
                bool[] data = mim.ReadCoils(0, 1);
                if (data[0])
                {
                    //실린더가 전진해있는 상태
                    label1.Text = "결과 : 전진";
                }
                else
                {
                    //후진해있는 상태
                    label1.Text = "결과 : 후진";
                }
                */
            }
            catch
            {
                MessageBox.Show("실패");
            }

        }

        private void label8_Click(object sender, EventArgs e)
        {

        }

        private void button8_Click(object sender, EventArgs e)
        {
            try
            {
                mim.WriteSingleCoil(3, true);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void button10_Click(object sender, EventArgs e)
        {
            try
            {
                mim.WriteSingleCoil(2, true);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void button11_Click(object sender, EventArgs e)
        {
            try
            {
                mim.WriteSingleCoil(2, false);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void button9_Click(object sender, EventArgs e)
        {
            try
            {
                mim.WriteSingleCoil(3, false);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void button12_Click(object sender, EventArgs e)
        {
            try
            {
                mim.WriteSingleCoil(4, true);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void button13_Click(object sender, EventArgs e)
        {
            try
            {
                mim.WriteSingleCoil(4, false);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void button14_Click(object sender, EventArgs e)
        {
            try
            {
                mim.WriteSingleCoil(5, true);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void button15_Click(object sender, EventArgs e)
        {
            try
            {
                mim.WriteSingleCoil(5, false);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void label2_Click(object sender, EventArgs e)
        {

        }

        private void Form1_Load(object sender, EventArgs e)
        {

        }

        private void button16_Click(object sender, EventArgs e)
        {
            try
            {
                mim.WriteSingleCoil(6, true);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void button17_Click(object sender, EventArgs e)
        {
            try
            {
                mim.WriteSingleCoil(6, false);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void button19_Click(object sender, EventArgs e)
        {
            try
            {
                mim.WriteSingleCoil(7, true);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void button18_Click(object sender, EventArgs e)
        {
            try
            {
                mim.WriteSingleCoil(7, false);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void groupBox4_Enter(object sender, EventArgs e)
        {

        }

        private void label16_Click(object sender, EventArgs e)
        {

        }

        private void button21_Click(object sender, EventArgs e)
        {
            try
            {
                mim.WriteSingleCoil(8, true);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void button20_Click(object sender, EventArgs e)
        {
            try
            {
                mim.WriteSingleCoil(8, false);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void button23_Click(object sender, EventArgs e)
        {
            try
            {
                mim.WriteSingleCoil(9, true);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void button22_Click(object sender, EventArgs e)
        {
            try
            {
                mim.WriteSingleCoil(9, false);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void button25_Click(object sender, EventArgs e)
        {
            try
            {
                mim.WriteSingleCoil(10, true);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void button24_Click(object sender, EventArgs e)
        {
            try
            {
                mim.WriteSingleCoil(10, false);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void groupBox3_Enter(object sender, EventArgs e)
        {

        }

        private void button27_Click(object sender, EventArgs e)
        {
            //3개의 램프를 다켠다
            try
            {
                bool[] state = {true, true, true};
                mim.WriteMultipleCoils(8, state);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void button26_Click(object sender, EventArgs e)
        {
            try
            {
                bool[] state = { false, false, false };
                mim.WriteMultipleCoils(8, state);
            }
            catch
            {
                MessageBox.Show("실패");
            }
        }

        private void button28_Click(object sender, EventArgs e)
        {
            //PLC에 값 쓰기
            try
            {
                ushort num = ushort.Parse(textBox2.Text);
                mim.WriteSingleRegister(0, num);

            }
            catch
            {
                // MessageBox.Show("실패");
            }
        }

        private void button29_Click(object sender, EventArgs e)
        {
            try
            {
                //레지스터 일기(홀딩레지스터)
             ushort[] data = mim.ReadHoldingRegisters(0, 1);

             label19.Text = data[0].ToString();
            }
            catch
            {

            }
        }

        private void button30_Click(object sender, EventArgs e)
        {
            //전체공정시작
            try
            {
                //100번지(쓰키코일0번지) 사각펄스 전송하기
                mim.WriteSingleCoil(0, false);
                mim.WriteSingleCoil(0, true);
                mim.WriteSingleCoil(0, false);

            }
            catch
            {

            }
        }

        private void button31_Click(object sender, EventArgs e)
        {
            //전체공정종료
            try
            {
                //100번지(쓰키코일0번지) 사각펄스 전송하기
                mim.WriteSingleCoil(1, false);
                mim.WriteSingleCoil(1, true);
                mim.WriteSingleCoil(1, false);

            }
            catch
            {

            }
        }
    }
}
