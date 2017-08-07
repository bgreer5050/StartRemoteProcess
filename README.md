# StartRemoteProcess



            var processName = "virtterm.exe";

            var connectoptions = new ConnectionOptions();
            connectoptions.Username = @"domain\username";
            connectoptions.Password = "password";

            string ipAddress = "10.0.100.200";
            ManagementScope scope = new ManagementScope(@"\\" + ipAddress + @"\root\cimv2", connectoptions);

            // WMI query
            var query = new SelectQuery("select * from Win32_process where name = '" + processName + "'");

            using (var searcher = new ManagementObjectSearcher(scope, query))
            {
                foreach (ManagementObject process in searcher.Get()) // this is the fixed line
                {
                    process.InvokeMethod("Terminate", null);
                }
            }
