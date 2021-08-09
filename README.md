# ScientificCalculator
## Scientific Calculator using C# Windows Form Application

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace ScientificCalculator
{
    public partial class Form1 : Form
    {
        double result = 0;
        string operation = "";
        bool enter_value = false;
        float celsius, fahrenheit, kelvin;
        char temperature;

        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)     // Form LOading
        {
            this.Width = 321;
            textBox1.Width = 286;
        }

        private void textBox1_TextChanged(object sender, EventArgs e)    // Condition for range of 12 digits
        {
            if (textBox1.Text.Length == 12)
            {
                MessageBox.Show("You Reach to mAximum number of length !! ");
            }
            if(textBox1.Text.Length > 12)
            {
                textBox1.Text = textBox1.Text.Substring(0, 12);
            }
        }

        private void standardToolStripMenuItem_Click(object sender, EventArgs e)  // Size for Standard Calculator
        {
            this.Width = 321;
            textBox1.Width = 286;
        }

        private void scientificToolStripMenuItem_Click(object sender, EventArgs e)   // Size of Scientific Calculator
        {
            this.Width = 627;
            textBox1.Width = 595;
        }

       
        private void temperatureToolStripMenuItem_Click(object sender, EventArgs e)  // Size for Temperature Calculator
        {
            this.Width = 988;
            textBox1.Width = 595;
            textBowConvert.Focus();
            grpTemperature.Visible = true;
            grptem2.Visible = true;
            grpMulti.Visible = false;

            grpTemperature.Location = new Point(628, 29);
            grpTemperature.Width = 332;
            grpTemperature.Height = 400;
        }

        private void multiplicationTableToolStripMenuItem_Click(object sender, EventArgs e)  // Size for Multiplication Table
        {
            this.Width = 988;
            textBox1.Width = 595;
            txtMultiply.Focus();

            grpTemperature.Visible = false;
            grptem2.Visible = false;
            grpMulti.Visible = true;

            grpMulti.Location = new Point(628, 29);
            grpMulti.Width = 332;
            grpMulti.Height = 400;

        }

       
        // Code for standard calculator

        private void button_click(object sender, EventArgs e)    // number butoon click (0 - 9)
        {
            if ((textBox1.Text == "0") || (enter_value))
            {
                textBox1.Text = "";
            }
            enter_value = false;
            Button num = (Button)sender;
            if (num.Text == ".")
            {
                if (!textBox1.Text.Contains("."))   // To check weather it Contains 'Zero' or not  
                {
                    textBox1.Text = textBox1.Text + num.Text;
                }
            }
            else
            {
                textBox1.Text = textBox1.Text + num.Text;
            }
        }

        private void operator_click(object sender, EventArgs e)   // operator click (+,-,*,/,mod, exp)
        {
            Button op = (Button)sender;
            if (result != 0)
            {
                Equal_button.PerformClick();
                operation = op.Text;
                label_currentOp.Text = result + " " + operation;
                enter_value = true;
            }
            else
            {
                operation = op.Text;
                result = Double.Parse(textBox1.Text);
                label_currentOp.Text = result + " " + operation;
                enter_value = true;
            }
            
        }


        private void CE_button_click(object sender, EventArgs e)  // clear button
        {
            textBox1.Text = "0";
        }

        private void C_button_click(object sender, EventArgs e)  // clear button - also clear history
        {
            textBox1.Text = "0";
            result = 0;
        }

        private void back_button_click(object sender, EventArgs e)  // backbutton click
        {
            textBox1.Text = (textBox1.Text.Length > 0) ? textBox1.Text.Substring(0, textBox1.Text.Length - 1) : "0";
          
            if(textBox1.Text == "")
            {
                textBox1.Text = "0";
            }
        }

        private void Equal_button_cilck(object sender, EventArgs e)   // Equal button
        { 
            switch (operation)
            {
                case "+":
                    textBox1.Text = (result + Double.Parse(textBox1.Text)).ToString();
                    break;
                case "-":
                    textBox1.Text = (result - Double.Parse(textBox1.Text)).ToString();
                    break;
                case "*":
                    textBox1.Text = (result * Double.Parse(textBox1.Text)).ToString();
                    break;
                case "/":
                    textBox1.Text = (result / Double.Parse(textBox1.Text)).ToString();
                    break;
                case "±":
                    result = double.Parse(textBox1.Text);
                    result = result * -1;
                    textBox1.Text = result.ToString();
                    break;
                case "mod":
                    textBox1.Text = (result % Double.Parse(textBox1.Text)).ToString();
                    break;
                case "Exp":
                    double l;
                    l = Math.Exp(Convert.ToDouble(textBox1.Text));
                    textBox1.Text = Convert.ToString(l);
                    break;
                default:
                    break;
            }
            result = Double.Parse(textBox1.Text);
            label_currentOp.Text = " ";
        }

        // Code for Scientific calculator

        private void pi_button_click(object sender, EventArgs e)  // PI button click
        {
            result = Math.PI;
            textBox1.Text = result.ToString();
        }

        private void log_click(object sender, EventArgs e)   // for log
        {
            try
            {
                if (textBox1.Text.Length != 0)
                {
                    result = double.Parse(textBox1.Text);
                    result = Math.Log10(result);
                    textBox1.Text = result.ToString();
                }
            }
            catch(Exception ex)
            {
                MessageBox.Show(ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
        }

        private void ln_click(object sender, EventArgs e)   // for lnx
        {   
            try{
                if (textBox1.Text.Length != 0)
                {
                    result = double.Parse(textBox1.Text);
                    result = Math.Log(result);
                    textBox1.Text = result.ToString();
                }
            }
            catch(Exception ex)
            {
                MessageBox.Show(ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
        }

        private void sqrt_click(object sender, EventArgs e)   // for sqrt
        {
            try
            {
                if (textBox1.Text.Length != 0)
                {
                    result = double.Parse(textBox1.Text);
                    result = Math.Sqrt(result);
                    textBox1.Text = result.ToString();
                }
            }
            catch(Exception ex)
            {
                MessageBox.Show(ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
        }

        private void pow_click(object sender, EventArgs e)   // for sqaure 
        {
            try
            {
                if (textBox1.Text.Length != 0)
                {
                    result = double.Parse(textBox1.Text);
                    result = Math.Pow(result, 2);
                    textBox1.Text = result.ToString();
                }
            }
            catch(Exception ex)
            {
                MessageBox.Show(ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
        }

        private void cube_click(object sender, EventArgs e)    // for cube 
        {
            try
            {
                if (textBox1.Text.Length != 0)
                {
                    result = double.Parse(textBox1.Text);
                    result = Math.Pow(result, 3);
                    textBox1.Text = result.ToString();
                }
            }
            catch(Exception ex)
            {
                MessageBox.Show(ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
        }

        private void divide_click(object sender, EventArgs e)   // for 1/x 
        {
            try
            {
                if (textBox1.Text.Length != 0)
                {
                    result = double.Parse(textBox1.Text);
                    result = 1 / (result);
                    textBox1.Text = result.ToString();
                }
            }
            catch(Exception ex)
            {
                MessageBox.Show(ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
        }

        private void percentage_click(object sender, EventArgs e)   // for percentage (x / 100)
        {
            try
            {
                if (textBox1.Text.Length != 0)
                {
                    result = double.Parse(textBox1.Text);
                    result = (result) / 100;
                    textBox1.Text = result.ToString();
                }
            }
            catch(Exception ex)
            {
                MessageBox.Show(ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
        }

        private void sin_click(object sender, EventArgs e)   // for sinx
        {
            try
            {
                if (textBox1.Text.Length != 0)
                {
                    result = double.Parse(textBox1.Text);
                    result = Math.Sin(result);
                    textBox1.Text = result.ToString();
                }
            }
            catch(Exception ex)
            {
                MessageBox.Show(ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
        }

        private void sinh_click(object sender, EventArgs e)   // for sinhx
        {
            try
            {
                if (textBox1.Text.Length != 0)
                {
                    result = double.Parse(textBox1.Text);
                    result = Math.Sinh(result);
                    textBox1.Text = result.ToString();
                }
            }
            catch(Exception ex)
            {
                MessageBox.Show(ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
        }

        private void cos_click(object sender, EventArgs e)  // for cosx
        {
            try
            {
                if (textBox1.Text.Length != 0)
                {
                    result = double.Parse(textBox1.Text);
                    result = Math.Cos(result);
                    textBox1.Text = result.ToString();
                }
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
        }

        private void cosh_click(object sender, EventArgs e)    // for coshx
        {
            try
            {
                if (textBox1.Text.Length != 0)
                {
                    result = double.Parse(textBox1.Text);
                    result = Math.Cosh(result);
                    textBox1.Text = result.ToString();
                }
            }
            catch(Exception ex)
            {
                MessageBox.Show(ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
        }

        private void tan_click(object sender, EventArgs e)    // for tanx
        {
            try
            {
                if (textBox1.Text.Length != 0)
                {
                    result = double.Parse(textBox1.Text);
                    result = Math.Tan(result);
                    textBox1.Text = result.ToString();
                }
            }
            catch(Exception ex)
            {
                MessageBox.Show(ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
        }

        private void tanh_click(object sender, EventArgs e)    // for tanhx
        {
            try
            {
                if (textBox1.Text.Length != 0)
                {
                    result = double.Parse(textBox1.Text);
                    result = Math.Tanh(result);
                    textBox1.Text = result.ToString();
                }
            }
            catch(Exception ex)
            {
                MessageBox.Show(ex.Message, "Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
            }
        }

        private void Bin_click(object sender, EventArgs e)    // for Binary number
        {
            int a = int.Parse(textBox1.Text);
            textBox1.Text = System.Convert.ToString(a, 2);  
        }

        private void Oct_click(object sender, EventArgs e)   // for Octal number
        {
            int a = int.Parse(textBox1.Text);
            textBox1.Text = System.Convert.ToString(a, 8);
        }

        private void Hex_click(object sender, EventArgs e)  // for Hexadecimal number
        {
            int a = int.Parse(textBox1.Text);
            textBox1.Text = System.Convert.ToString(a, 16);
        }

        private void Dec_click(object sender, EventArgs e)   // for Decimal number
        {
            int a = int.Parse(textBox1.Text);
            textBox1.Text = System.Convert.ToString(a);
        }
        
        //  Code for temperature calculator....

        private void rbCeltoFrh_CheckedChanged(object sender, EventArgs e)
        {
            temperature = 'C';
        }

        private void rbFhrToCel_CheckedChanged(object sender, EventArgs e)
        {
            temperature = 'F';
        }
                                   
        private void rbKelvin_CheckedChanged(object sender, EventArgs e)
        {
            temperature = 'K';
        }

        private void convert_click(object sender, EventArgs e)  // for convert button 
        {
            switch (temperature)
            {
                case 'C':  // Celsius To Fahrenheit
                    celsius = float.Parse(textBowConvert.Text);
                    txtConvert.Text = ((((9 * celsius) / 5) + 32).ToString());
                    break;
                case 'F':  // Fahrenheit to Celsius
                    fahrenheit = float.Parse(textBowConvert.Text);
                    txtConvert.Text = ((((fahrenheit - 32) * 5) / 9).ToString());
                    break;
                case 'k':  // Kelvin
                    kelvin = float.Parse(textBowConvert.Text);
                    txtConvert.Text = (((((9 * kelvin) / 5) + 32) +273.15).ToString());
                    break;
               
            }
        }

        private void reset_button_click(object sender, EventArgs e)  // for Reset Temperature
        {
            textBowConvert.Clear();
            txtConvert.Text = " ";
            rbCeltoFrh.Checked = false;
            rbFhrToCel.Checked = false;
            rbKelvin.Checked = false;
        }

        // Code for Multipication Table Calculator...

        private void btn_Multiply_Click(object sender, EventArgs e)    // Multiply button_click
        {
            int a = Convert.ToInt32(txtMultiply.Text);
            for (int i = 1; i <= 10; i++)
            {
                lstMultiplication.Items.Add(i + "x" + a + "=" + a * i);

            }
        }

        private void btn_resetMult_Click(object sender, EventArgs e)    // for Reset Multiplication number
        {
            txtMultiply.Clear();
            lstMultiplication.Items.Clear();
        }

        // For Application Closing.....
        private void exitToolStripMenuItem_Click(object sender, EventArgs e)
        {
            Application.Exit();
        }

    }
    
}
