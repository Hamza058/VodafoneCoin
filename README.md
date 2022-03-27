# VodafoneCoin
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.Data.SqlClient;

namespace Vodafon
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        SqlConnection con;
        SqlCommand cmd;
        SqlDataReader dr;

        public static string isim = "";
        public static string soyisim = "";
        public static string dakika = "";
        public static string coin = "";
        public static string sms = "";
        public static string net = "";
        public static string telefon = "";


        private void button1_Click(object sender, EventArgs e)
        {
            Form5 gec = new Form5();

            if (textBox1.Text.Trim() == "")
            {
                MessageBox.Show("Lütfen Bilgilerinizi Giriniz", "HATA", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
            else
            {
                con = new SqlConnection("Data Source=HKILIC\\SQLEXPRESS;Initial Catalog=Vodafon;Integrated Security=True");
                cmd = new SqlCommand();
                con.Open();
                cmd.Connection = con;
                cmd.CommandText = "SELECT * FROM Deneme where Telefon='" + textBox1.Text+"'";
                dr = cmd.ExecuteReader();
                if (dr.Read())
                {
                    isim = dr[1].ToString();
                    soyisim = dr[2].ToString();
                    telefon = dr[3].ToString();
                    coin = dr[8].ToString();
                    dakika = dr[5].ToString();
                    sms = dr[6].ToString();
                    net = dr[7].ToString();
                    MessageBox.Show("Tebrikler! Başarılı bir şekilde giriş yaptınız.");
                    gec.Show();
                    this.Hide();
                }
                else
                {
                    MessageBox.Show("Telefon numaranızı kontrol ediniz. Kayıtlı Kullanıcılar 123, 321, 456");
                }
                con.Close();
            }
        }

        private void pictureBox2_Click(object sender, EventArgs e)
        {
            Application.Exit();
        }

        #region Form Hareketleri
        int hareket;
        int Mouse_X;
        int Mouse_Y;

        private void Form1_MouseUp(object sender, MouseEventArgs e)
        {
            hareket = 0;
        }

        private void Form1_MouseDown(object sender, MouseEventArgs e)
        {
            hareket = 1;
            Mouse_X = e.X;
            Mouse_Y = e.Y;
        }

        private void Form1_MouseMove(object sender, MouseEventArgs e)
        {
            if (hareket == 1)
            {
                this.SetDesktopLocation(MousePosition.X - Mouse_X, MousePosition.Y - Mouse_Y);
            }
        }
        #endregion
    }
}
