using System;
using System.Windows.Forms;

namespace CalculadoraDesktop
{
    public class CalculadoraForm : Form
    {
        private TextBox display;
        private double valor1, valor2;
        private string operacao;

        public CalculadoraForm()
        {
            this.Text = "Calculadora em C#";
            this.Width = 300;
            this.Height = 400;

            display = new TextBox { Left = 10, Top = 10, Width = 260 };
            this.Controls.Add(display);

            string[] botoes = { "7", "8", "9", "/", "4", "5", "6", "*",
                                "1", "2", "3", "-", "0", "C", "=", "+" };

            int left = 10, top = 50;

            for (int i = 0; i < botoes.Length; i++)
            {
                var btn = new Button
                {
                    Text = botoes[i],
                    Left = left,
                    Top = top,
                    Width = 60,
                    Height = 40
                };
                btn.Click += BotaoClick;
                this.Controls.Add(btn);

                left += 65;
                if ((i + 1) % 4 == 0)
                {
                    left = 10;
                    top += 45;
                }
            }
        }

        private void BotaoClick(object sender, EventArgs e)
        {
            var botao = (Button)sender;
            string texto = botao.Text;

            if ("0123456789".Contains(texto))
            {
                display.Text += texto;
            }
            else if ("+-*/".Contains(texto))
            {
                valor1 = double.Parse(display.Text);
                operacao = texto;
                display.Text = "";
            }
            else if (texto == "=")
            {
                valor2 = double.Parse(display.Text);
                switch (operacao)
                {
                    case "+": display.Text = (valor1 + valor2).ToString(); break;
                    case "-": display.Text = (valor1 - valor2).ToString(); break;
                    case "*": display.Text = (valor1 * valor2).ToString(); break;
                    case "/": display.Text = (valor2 != 0 ? (valor1 / valor2).ToString() : "Erro"); break;
                }
            }
            else if (texto == "C")
            {
                display.Text = "";
                valor1 = valor2 = 0;
                operacao = "";
            }
        }

        [STAThread]
        static void Main()
        {
            Application.EnableVisualStyles();
            Application.Run(new CalculadoraForm());
        }
    }
}
