## WPF中的自定义UserControl的快速集成

1. 按照标准的方式开发居于WPF的控件
只需要在控件的类中实现如下方法，就可以集成到SensingPlatform平台,Initialize可以初始化有关配置，StartPage，整个页面启动时的事件监听，StopPage，整个页面离开时的监听
```C#
public void Initialize(XElement config)
        {
            if (config != null)
            {
                //Output.Text += config.ToString();
            }
        }

        public void StartPage(string query)
        {
            if (!string.IsNullOrEmpty(query))
            {
                //Output.Text += query + Environment.NewLine;
            }
        }

        public void StopPage(string query)
        {
            if (!string.IsNullOrEmpty(query))
            {
                //Output.Text += query + Environment.NewLine;
            }
        }
```
2. 配置用户自定义的控件到平台的页面上，在配置的区域，可传入相关的配置，可实现灵活的功能 
