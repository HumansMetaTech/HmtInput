# Hmt Input
A clean, simple, and tiny library to detect user input like Keyboard and Mouse.

[Humans Meta Tech](https://humansmeta.tech)

You can track the activity of the user using mouse and keyboard activity. This will track the last activity of the mouse and keyboard since last used using timeframe.

## How to Use it?

First, you need to add a reference of the **HmtInput.dll** library to your project which is present in this location `\bin\Debug\netstandard2.0\HmtInput.dll` or you can install this package using **Nuget Package Manager**.

Then create a new class of your own and refer to different methods from the `HmtInput.dll` library.
```
using HmtInput;
using System;
using System.Windows.Forms;
public class User
{
    private System.Windows.Forms.Timer timer;
    private InputSources LastInput;

    public User()
    {
        LastInput = new InputSources();
        this.timer = new System.Windows.Forms.Timer();
        this.timer.Interval = new TimeSpan(0, 0, 0, 0, 100).Milliseconds;
        this.timer.Tick += timer_Tick;
        this.timer.Start();
    }

    private void timer_Tick(object sender, EventArgs e)
    {
        TimeSpan time = DateTime.Now.AddMinutes(1) - this.LastInput.GetLastInputTime();
        if (time.Minutes > 1)
        {
            this.timer.Stop();
            var result = MessageBox.Show("Are you Active?", "Checkpoint", MessageBoxButtions.YesNo, MessageBoxIcon.Question);
            if (result == DialogResult.No)
            {
                /* Do something big here */
                return;
            }
            this.timer.Start();
        }
    }
}
```
In the above code, an event `timer_Tick` is activated from the class constructor. Its interval is set to `0.1 Sec`. This means the timer will check the mouse or keyboard activity after every `0.1 Sec`. 

You can set the duration in the if condition from `1 Min` to any as you require.

After completing this code, create an object of this class like `User` in this example to the main form or anywhere else in your code to start tracking.

We hope this will be helpful to you.

Have any issues? Raise an [Issue](https://github.com/HumansMetaTech/HmtInput/issues)
