# Create Automations on Make.com

Make.com is a powerful integration platform that lets you connect your favorite apps and services to automate repetitive tasks. Build custom workflows to streamline your work, boost productivity, and free yourself from manual busywork. Make.com integrates with thousands of popular tools, making it easy to automate tasks across your entire workflow.

Before starting this Pico LTE tutorial, the Pico LTE SDK installation and configuration steps must be completed. Below are the system requirements for this tutorial. If you haven't followed the SDK installation steps, please refer to the page below before proceeding with the tutorial. The details of these steps will not be covered in this tutorial.

## System Requirements

| Hardware Requirements | Software Requirements | 
| --------------------- | --------------------- |
| Sixfab Pico LTE       | Thonny IDE            |
| Micro USB Cable       |                       | 

If you have completed all the requirements, you are ready to create automations on Make.com with the Pico LTE device.

Let's get started!

## Preparing Coding Environment

1. Download the [Pico LTE SDK repository](https://github.com/sixfab/pico_lte_micropython-sdk) to your local machine. If you have already downloaded it, skip this step. 
2. Open script **"examples → make_automation → create_event.py / get_weather.py"** from the repository via Thonny IDE.
3. If you haven't, create a ``config.json`` file in the root directory of Pico LTE device.

## Get weather forecast using Make Automation.

1. Login to Make.com 

    Login to your Make.com account from [the login page](https://www.make.com/en/login), if you do not have an account, create a new account from the [registration page](https://www.make.com/en/register?). You can answer the questions during registration as you wish.

2. Create a New Scenario 
   
   Press on the **"Create a new scenario "** button.

   ![](images/get_weather-images/create_new_scenario.png)

3. Prepare First Module (Webhooks)

    Press the plus bubble in the centre of the page. Enter "Webhooks" in the search field. Then select the **Webhooks** module.

    ![](images/get_weather-images/webhook_module.png)

    Select **"Custom webhook "** under the Triggers heading.

    ![](images/get_weather-images/webhook_module_2.png)

    Press **"Create a webhook"** button and name it. 

    ![](images/get_weather-images/webhook_module_3.png)
    ![](images/get_weather-images/webhook_module_4.png)

    The picture below shows that the webhook module is in listening mode to access the names of the variables you send. In this case, you need to run **"examples → make_automation → get_weather.py "** once from the repository via Thonny IDE. Keep the webhook url that appears here for running the code. To run the code, go to [**Test the code example**](#test-the-code-example) heading and after running it back continue from here. 

    ![](images/get_weather-images/webhook_module_5.png)

    After the code runs successfully, **"Succesfully determined"** appears. And you can continue to add the next module. 

    ![](images/get_weather-images/webhook_module_6.png)

4. Prepare Second Module (Weather)

    Press the small plus bubble next to the webhook module. Enter "Weather" in the search field. Then select the **Weather** module.

    ![](images/get_weather-images/add_module.png)
    ![](images/get_weather-images/weather_module.png)

    Select **"Get daily weather forecast"** under the Actions heading.

    ![](images/get_weather-images/weather_module_2.png)

    Here you can get the weather forecast as often as you want. For this example, select **"tomorrow "** under the "Days" heading. Also assign the City value entered by the user from the part shown with 2 for the city. If you do not see any variable in the menu shown with 2, please refer to [**Troubleshooting**](#troubleshooting).

    ![](images/get_weather-images/weather_module_3.png)


4. Prepare Third Module (Webhooks)

    Press the small plus bubble next to the webhook module. Then select the **Webhooks** module.

    ![](images/get_weather-images/response_webhook_module.png)

    Select **"Webhook Response"** under the Actions heading.

    ![](images/get_weather-images/response_webhook_module_2.png)

    This is the part where the information from Weather and Webhooks modules will be displayed to the user. For this example, it is filled like the field shown with 1 and also you can fill with the following text. It can be changed according to user's request.

    ```
    City: {{1.City}} --- Tomorrow's Temperature: {{2.temperature.day}} --- Wind Speed: {{2.wind.speed}} --- Air Humidity: {{2.humidity}} --- General Description: {{2.description}} 
    ```

    ![](images/get_weather-images/response_webhook_module_3.png)

## Test the Code Example 

1. Copy the following code block into the config.json file and enter your webhook url.
   
   ```
   {
    "make_automation":{
            "url": "[INCOMING_WEBHOOK_URL]",
        }
   } 
   ```
2. Open script "examples → google_sheets → get_weather.py" from the repository via Thonny IDE. 
3. Set the City value you want to get weather forecast for tomorrow. Run the **"get_weather.py"**. 

    ![](images/get_weather-images/get_weather_thonny.png)
4. The output you get in the code should look like this for City = Adana:

    ```
    MPY: soft reboot
    INFO: Getting the forecast for tomorrow.
    INFO: Result:  {'status': 0, 'response': ["City : Adana --- Tomorrow's temperature : 26.59 --- Wind Speed : 4.3 --- Air Humidity : 37 --- Description : scattered clouds.", 'OK', '+QHTTPREAD: 0'], 'interval': 0}
    ```

5. If you want to see the progress of the automation system on the make.com site, firstly, put the system into listening mode by pressing the **"Run once "** button at the bottom left.

    ![](images/get_weather-images/automation_system.png)

6. After the system is in listening mode, you can run the **get_weather.py** file. After running successfully, it looks like the picture below.

    ![](images/get_weather-images/automation_system_success.png)

## Troubleshooting

1. If you can't see the variables from the Webhooks module (background coloured in red) while filling in the fields in the **second module (Weather)**, click on the **"Webhooks "** module and click on the **"Redeterimine data structure "** button and then run **get_weather.py** as shown below. After the code runs successfully, **"Succesfully determined"** appears. After saving the scenario and refreshing the page, you can now see your variables in the relevant fields. 

    ![](images/get_weather-images/troubleshooting.png)
