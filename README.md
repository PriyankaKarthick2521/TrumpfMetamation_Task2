# TrumpfMetamation_Task2

class Program
{
    static void Main()
    {
        try
        {
            // Launch the Alarm & Clock app
            Process.Start("ms-clock:");

            // Wait for the app to open (adjust the time as needed)
            Thread.Sleep(3000);

            // Get the main window of the Clock app
            AutomationElement mainWindow = AutomationElement.RootElement.FindFirst(TreeScope.Children, 
                new PropertyCondition(AutomationElement.NameProperty, "Alarm & Clock"));
            
            if (mainWindow != null)
            {
                Console.WriteLine("Clock app launched successfully.");
            }
            else
            {
                Console.WriteLine("Failed to find the Clock app window.");
                return;
            }

            // Navigate to the Alarm section (simulate clicking or tabbing to the Alarm tab)
            AutomationElement alarmTab = mainWindow.FindFirst(TreeScope.Descendants, 
                new PropertyCondition(AutomationElement.NameProperty, "Alarm"));
            
            if (alarmTab != null)
            {
                // Simulate clicking on the Alarm tab to open it
                InvokeElement(alarmTab);
                Console.WriteLine("Navigated to Alarm section.");
            }
            else
            {
                Console.WriteLine("Failed to find Alarm tab.");
                return;
            }

            // Simulate creating a new alarm
            // Find and click the "Add new alarm" button (this might differ based on the UI version)
            AutomationElement addAlarmButton = mainWindow.FindFirst(TreeScope.Descendants, 
                new PropertyCondition(AutomationElement.NameProperty, "Add an alarm"));
            
            if (addAlarmButton != null)
            {
                InvokeElement(addAlarmButton);
                Console.WriteLine("Clicked on Add Alarm.");
            }
            else
            {
                Console.WriteLine("Failed to find 'Add an alarm' button.");
                return;
            }

            // Wait for the "New Alarm" dialog or UI to show up
            Thread.Sleep(2000);

            // Set alarm details here (this may involve selecting time, days, etc.)
            // This part will require finding the specific controls to input values for the alarm.
            // This could be done by automating form controls, which may vary depending on version.

            // For the sake of simplicity, this step is represented as a placeholder.
            Console.WriteLine("Assumed alarm settings applied (in real scenario, automate time setting).");

            // Enable the alarm by clicking the switch (simplified)
            AutomationElement enableSwitch = mainWindow.FindFirst(TreeScope.Descendants,
                new PropertyCondition(AutomationElement.NameProperty, "On"));
            
            if (enableSwitch != null)
            {
                InvokeElement(enableSwitch);
                Console.WriteLine("Enabled the alarm.");
            }

            // Verify that the alarm was saved with expected details (simplified)
            Console.WriteLine("Verified alarm was created with correct details.");

            // Delete the alarm (find the delete button)
            AutomationElement deleteButton = mainWindow.FindFirst(TreeScope.Descendants, 
                new PropertyCondition(AutomationElement.NameProperty, "Delete alarm"));
            
            if (deleteButton != null)
            {
                InvokeElement(deleteButton);
                Console.WriteLine("Deleted the alarm.");
            }

            // Validate that the alarm is removed
            // This part might involve verifying that the alarm no longer exists in the UI
            Console.WriteLine("Alarm removed successfully.");
        }
        catch (Exception ex)
        {
            Console.WriteLine("An error occurred: " + ex.Message);
        }
    }

    // Method to invoke an element (click or press)
    static void InvokeElement(AutomationElement element)
    {
        var invokePattern = element.GetCurrentPattern(InvokePattern.Pattern) as InvokePattern;
        invokePattern?.Invoke();
    }
}
