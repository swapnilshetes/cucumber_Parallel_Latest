AppiumDriverContext.java

/**
 * 
 */
package com.indecomm.api;

import java.io.File;
import java.io.FileReader;

/**
 * @author navjotkochar
 */

import java.io.IOException;
import java.net.URL;
import java.util.ArrayList;
import java.util.List;
import java.util.Map;
import java.util.Scanner;
import java.util.concurrent.TimeUnit;

import org.json.simple.JSONArray;
import org.json.simple.JSONObject;
import org.json.simple.parser.ContainerFactory;
import org.json.simple.parser.JSONParser;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.remote.DesiredCapabilities;

import com.mongodb.util.JSON;

import io.appium.java_client.AppiumDriver;
import io.appium.java_client.android.AndroidDriver;
import io.appium.java_client.ios.IOSDriver;
import io.appium.java_client.remote.IOSMobileCapabilityType;

public class AppiumDriverContext {
	// public static IOSDriverContext driverContext;
	public static AppiumDriver driver;
	static JSONParser parser = new JSONParser();

	public static AppiumDriver getDriver(String device, String OSwithDevice) throws IOException {
		org.json.simple.JSONObject jsonObject = null;
		org.json.simple.JSONObject jsonObject1 = null;
		org.json.simple.JSONObject jsonObject2 = null;
		try {

			String cwd = System.getProperty("user.dir") + "/feedFiles/DeviceCababilities.json";
			Object obj = parser.parse(new FileReader(cwd));
			jsonObject = (JSONObject) obj;
			// System.out.println(cwd);
			jsonObject1 = (JSONObject) jsonObject.get(OSwithDevice);
			System.out.println("SAME ==" + jsonObject1);
			jsonObject2 = (JSONObject) jsonObject1.get("capabilities");

		} catch (Exception e) {
			e.printStackTrace();
		}

		if (device.equalsIgnoreCase("Android")) {

			if (driver == null) {

				DesiredCapabilities desiredCapabilities = new DesiredCapabilities();
				desiredCapabilities.setCapability("platformName", jsonObject2.get("platformName").toString());
				desiredCapabilities.setCapability("platformVersion", jsonObject2.get("version").toString());
				desiredCapabilities.setCapability("deviceName", jsonObject2.get("device").toString());
				desiredCapabilities.setCapability("appWaitActivity",
						"SplashActivity, SplashActivity,OtherActivity, *, *.SplashActivity");
				desiredCapabilities.setCapability("app", jsonObject2.get("app").toString());
				// desiredCapabilities.setCapability("appPackage",
				// jsonObject2.get("app_package").toString());
				// desiredCapabilities.setCapability("appActivity",
				// jsonObject2.get("activity").toString());
				driver = new AppiumDriver(new URL(jsonObject2.get("appiumServer").toString()), desiredCapabilities);
				driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
			}
		}

		return driver;

	}

	public static void closeDriver() {
		if (null != driver) {
			// driver.resetApp();
			driver.closeApp();
			driver.launchApp();
			// driver = null;
		}
	}

}


****************** LoginTestAndroid.java 

package com.indecomm.scripts.el;

import static org.junit.Assert.assertEquals;
import static org.junit.Assert.assertSame;
import static org.junit.Assert.assertTrue;

import org.openqa.selenium.WebElement;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

import com.indecomm.api.AppiumDriverContext;
import com.indecomm.pages.LoginTestAndroidTest;

import cucumber.api.java.en.Given;
import cucumber.api.java.en.Then;
import cucumber.api.java.en.When;
import io.appium.java_client.AppiumDriver;
import io.appium.java_client.MobileBy;
import junit.framework.Assert;

public class LoginTestAndroid {

	AppiumDriver driver;
	LoginTestAndroidTest loginTestAndroidTest;

	@Given("^User is on Home Page$")
	public void user_is_on_Home_Page() throws Throwable {
		System.out.println("First Test ");
		driver = new AppiumDriverContext().getDriver("Android", "Android_Andy");
		System.out.println("First Test Android_Andy +++++" + driver);
		System.out.println("Foirst End");

		loginTestAndroidTest = new LoginTestAndroidTest(driver);

		// assertEquals(loginTestAndroidTest.getLandingPageMessage(),"Welcome to
		// Electrolux");

		// Write code here that turns the phrase above into concrete actions
		// throw new PendingException();
	}

	@When("^User Navigate to LogIn Page$")
	public void user_Navigate_to_LogIn_Page() throws Throwable {

		Thread.sleep(4000);
		loginTestAndroidTest.ClickMe();
		// System.out.println(this.driver1.getContext());
		//assertTrue(loginTestAndroidTest.getLandingPageDisplay().isDisplayed());
		
		// Write code here that turns the phrase above into concrete actions
		// throw new PendingException();
	}

	@When("^User enters UserName and Password$")
	public void user_enters_UserName_and_Password() throws Throwable {
		
		System.out.println("Android_Andy Test 3");

	}

	@Then("^Message displayed Login Successfully$")
	public void message_displayed_Login_Successfully() throws Throwable {
		// Write code here that turns the phrase above into concrete actions
		System.out.println("Android_Andy Test 4");
		// throw new PendingException();
	}
}


************* LoginTestAndroidTest.java

package com.indecomm.pages;

import static org.junit.Assert.assertTrue;

import org.openqa.selenium.support.PageFactory;

import io.appium.java_client.AppiumDriver;
import io.appium.java_client.MobileElement;
import io.appium.java_client.pagefactory.AndroidFindBy;
import io.appium.java_client.pagefactory.AppiumFieldDecorator;
import io.appium.java_client.pagefactory.iOSFindBy;
import junit.framework.Assert;

public class LoginTestAndroidTest {

	AppiumDriver driver;

	/*private static final String ANDROID_LANDING_PAGE_MESSAGE = "new UiSelector().index(5)";

	private static final String ANDROID_HOME_CONTINUE = "new UiSelector().index(5)";
	*/
	
	
	@AndroidFindBy(xpath = ".//android.view.View[@content-desc=\"CONTINUE\"]")
	MobileElement btnCont;
	
	/*
	 * private static final String ANDROID_HOME_CONTINUE =
	 * "\"new UiSelector().index(5)\""; private static final String
	 * IOS_ACQUAINTANCE_EDIT_BUTTON = "Edit"; private static final String
	 * ANDROID_ACQUAINTANCE_DELETE_BUTTON =
	 * "new UiSelector().resourceIdMatches(\".*id/acquaintanceDeleteButton.*\")";
	 */

	/*@AndroidFindBy(uiAutomator = "new UiSelector().index(1)")
	MobileElement landingPageMsg;*/

	//@AndroidFindBy(uiAutomator = ANDROID_HOME_CONTINUE)
	

	// @AndroidFindBy(xpath="//android.view.View[@content-desc=\"CONTINUE\"]")

	// private static final String IOS_ACQUAINTANCE_EDIT_BUTTON = "Edit";

	// @iOSBy(accessibility = IOS_ACQUAINTANCE_EDIT_BUTTON)
	// private MobileElement acquaintanceEditButtonElement;

	public LoginTestAndroidTest(AppiumDriver driver1) {

		PageFactory.initElements(new AppiumFieldDecorator(driver1), this);

	}

	public MobileElement getLandingPageDisplay() throws InterruptedException {

		return btnCont;
	}

	public void ClickMe() throws InterruptedException {

		btnCont.click();
	}

}


********* DeviceCababilities.json
{
	"Android_Andy": {
		"capabilities": {
			"platformName": "Android",
			"device": "192.168.235.101:5555",
			"app": "C:\\Application\\Test.apk",
			"app_package": "com.electrolux.test",
			"activity": "com.electrolux.test",
			"version": "5.0",
			"appiumServer": "http://127.0.0.1:4767/wd/hub",
			"port": "4767",
			"deviceudid": "192.168.235.101:5555",
			"bundleid": "com.electrolux.test"
			}
	},
	"Android_Simulater": {
	"capabilities": {
			"platformName": "Android",
			"device": "192.168.235.102:5555",
			"app": "C:\\Application\\Test.apk",
			"app_package": "com.electrolux.test",
			"activity": "com.electrolux.test",
			"version": "7.0",
			"appiumServer": "http://127.0.0.1:4767/wd/hub",
			"port": "4766",
			"deviceudid": "192.168.235.102:5555",
			"bundleid": "com.electrolux.test"
			}
	}
}


******** POM ***********


<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>Cucumber_Selenium</groupId>
	<artifactId>Cucumber_Selenium</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>


	<name>Cucumber_Selenium</name>
	<url>http://maven.apache.org</url>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
	</properties>

	<build>
		<plugins>
			<plugin>
				<groupId>org.jenkins-ci.tools</groupId>
				<artifactId>maven-hpi-plugin</artifactId>
				<version>1.95</version>
			</plugin>

			<!-- <plugin> <groupId>org.apache.maven.plugins</groupId> <artifactId>maven-surefire-plugin</artifactId> 
				<version>2.22.0</version> <configuration> <suiteXmlFiles> <suiteXmlFile>testng.xml</suiteXmlFile> 
				</suiteXmlFiles> </configuration> </plugin> -->

			<plugin>
				<groupId>com.github.temyers</groupId>
				<artifactId>cucumber-jvm-parallel-plugin</artifactId>
				<version>2.1.0</version>
				<executions>
					<execution>
						<id>generateRunners</id>
						<phase>generate-test-sources</phase>
						<goals>
							<goal>generateRunners</goal>
						</goals>
						<configuration>

							<glue>com.indecomm.scripts.el</glue>
							<outputDirectory>${project.build.directory}/generated-test-sources/cucumber</outputDirectory>
							<featuresDirectory>src/test/resources/features</featuresDirectory>

							<cucumberOutputDir>target/cucumber-parallel</cucumberOutputDir>
							<format>json</format>

							<strict>true</strict>

							<monochrome>true</monochrome>

							<filterFeaturesByTags>false</filterFeaturesByTags>

							<useTestNG>false</useTestNG>

							<namingScheme>simple</namingScheme>

							<namingPattern>Parallel{c}IT</namingPattern>

							<parallelScheme>SCENARIO</parallelScheme>

							<!-- <customVmTemplate>src/test/resources/cucumber-custom-runner.vm</customVmTemplate> -->

						</configuration>
					</execution>
				</executions>
			</plugin>

			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-surefire-plugin</artifactId>
				<version>2.19.1</version>
				<configuration>
					<source>1.8</source>
					<target>1.8</target>
					<forkCount>5</forkCount>
					<reuseForks>true</reuseForks>
					<includes>
						<include>**/*IT.class</include>
					</includes>
				</configuration>
			</plugin>


		</plugins>
	</build>

	<dependencies>
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>4.12</version>
			<scope>test</scope>
		</dependency>

		<!-- https://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-java -->
		<!-- <dependency> <groupId>org.seleniumhq.selenium</groupId> <artifactId>selenium-java</artifactId> 
			<version>3.4.0</version> </dependency> -->
		<!-- https://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-java -->
		<dependency>
			<groupId>org.seleniumhq.selenium</groupId>
			<artifactId>selenium-java</artifactId>
			<version>3.14.0</version>
		</dependency>

		<!-- https://mvnrepository.com/artifact/info.cukes/cucumber-java -->
		<dependency>
			<groupId>info.cukes</groupId>
			<artifactId>cucumber-java</artifactId>
			<version>1.2.5</version>
		</dependency>

		<!-- https://mvnrepository.com/artifact/info.cukes/cucumber-jvm-deps -->
		<dependency>
			<groupId>info.cukes</groupId>
			<artifactId>cucumber-jvm-deps</artifactId>
			<version>1.0.5</version>
			<scope>provided</scope>
		</dependency>

		<!-- https://mvnrepository.com/artifact/info.cukes/cucumber-junit -->
		<dependency>
			<groupId>info.cukes</groupId>
			<artifactId>cucumber-junit</artifactId>
			<version>1.2.5</version>
			<scope>test</scope>
		</dependency>

		<dependency>
			<groupId>com.vimalselvam</groupId>
			<artifactId>cucumber-extentsreport</artifactId>
			<version>3.0.2</version>
		</dependency>

		<dependency>
			<groupId>com.aventstack</groupId>
			<artifactId>extentreports</artifactId>
			<version>3.1.2</version>
		</dependency>





		<!-- <dependency> <groupId>com.vimalselvam</groupId> <artifactId>cucumber-extentsreport</artifactId> 
			<version>3.1.1</version> </dependency> https://mvnrepository.com/artifact/com.aventstack/extentreports 
			<dependency> <groupId>com.aventstack</groupId> <artifactId>extentreports</artifactId> 
			<version>3.1.5</version> <scope>provided</scope> </dependency> -->

		<!-- https://mvnrepository.com/artifact/io.appium/java-client -->
		<dependency>
			<groupId>io.appium</groupId>
			<artifactId>java-client</artifactId>
			<version>6.1.0</version>
		</dependency>

		<!-- https://mvnrepository.com/artifact/org.apache.httpcomponents/httpcore -->
		<dependency>
			<groupId>org.apache.httpcomponents</groupId>
			<artifactId>httpcore</artifactId>
			<version>4.4.6</version>
		</dependency>

		<!-- https://mvnrepository.com/artifact/com.tngtech.java/junit-dataprovider -->
		<dependency>
			<groupId>com.tngtech.java</groupId>
			<artifactId>junit-dataprovider</artifactId>
			<version>1.13.1</version>
			<scope>test</scope>
		</dependency>

		<dependency>
			<groupId>com.github.temyers</groupId>
			<artifactId>cucumber-jvm-parallel-plugin</artifactId>
			<version>2.1.0</version>
		</dependency>

		<dependency>
			<groupId>com.googlecode.json-simple</groupId>
			<artifactId>json-simple</artifactId>
			<version>1.1.1</version>
		</dependency>
	</dependencies>



	<profiles>
		<profile>
			<id>Cucumber_Selenium</id>
			<build>
				<plugins>
					<plugin>
						<groupId>org.apache.maven.plugins</groupId>
						<artifactId>maven-failsafe-plugin</artifactId>
						<configuration>
							<parallel>none</parallel>
							<threadCount>6</threadCount>
							<disableXmlReport>true</disableXmlReport>
						</configuration>
						<executions>
							<execution>
								<id>runner.testrunner</id>
								<phase>Cucumber_Selenium</phase>
								<goals>
									<goal>Cucumber_Selenium</goal>
								</goals>
							</execution>
						</executions>
					</plugin>
				</plugins>
			</build>
		</profile>
	</profiles>
</project>
