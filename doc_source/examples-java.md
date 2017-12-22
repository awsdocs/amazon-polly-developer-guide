# Java Example<a name="examples-java"></a>

This example shows how to use Amazon Polly to stream speech from a Java\-based application\. The example uses the [AWS SDK for Java](https://aws.amazon.com/documentation/sdk-for-java/) to read the specified text using a voice selected from a list\.

The code shown covers major tasks, but does only minimal error checking\. If Amazon Polly encounters an error, the application terminates\. 

To run this example application, you need the following:

+  Java 8 Java Development Kit \(JDK\) 

+  [AWS SDK for Java ](https://aws.amazon.com/documentation/sdk-for-java/) 

+  [Apache Maven](http://maven.apache.org/) 

**To test the application**

1. Ensure that the JAVA\_HOME environment variable is set for the JDK\.

   For example, if you installed JDK 1\.8\.0\_121 on Windows at `C:\Program Files\Java\jdk1.8.0_121`, you would type the following at the command prompt:

   ```
   set JAVA_HOME=""C:\Program Files\Java\jdk1.8.0_121""
   ```

   If you installed JDK 1\.8\.0\_121 in Linux at `/usr/lib/jvm/java8-openjdk-amd64` , you would type the following at the command prompt: 

   ```
   export JAVA_HOME=/usr/lib/jvm/java8-openjdk-amd64
   ```

1. Set the Maven environment variables to run Maven from the command line\. 

   For example, if you installed Maven 3\.3\.9 on Windows at `C:\Program Files\apache-maven-3.3.9`, you would type the following:

   ```
   set M2_HOME=""C:\Program Files\apache-maven-3.3.9""
   set M2=%M2_HOME%\bin
   set PATH=%M2%;%PATH%
   ```

   If you installed Maven 3\.3\.9 on Linux at `/home/ec2-user/opt/apache-maven-3.3.9`, you would type the following:

   ```
   export M2_HOME=/home/ec2-user/opt/apache-maven-3.3.9
   export M2=$M2_HOME/bin
   export PATH=$M2:$PATH
   ```

1. Create a new directory called `polly-java-demo`\. 

1. In the `polly-java-demo` directory, create a new file called `pom.xml`, and paste the following code into it: 

   ```
   <project xmlns="http://maven.apache.org/POM/4.0.0" 
                       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
   	<modelVersion>4.0.0</modelVersion>
   	<groupId>com.amazonaws.polly</groupId>
   	<artifactId>java-demo</artifactId>
   	<version>0.0.1-SNAPSHOT</version>
   
   	<dependencies>
   		<!-- https://mvnrepository.com/artifact/com.amazonaws/aws-java-sdk-polly -->
   		<dependency>
   			<groupId>com.amazonaws</groupId>
   			<artifactId>aws-java-sdk-polly</artifactId>
   			<version>1.11.77</version>
   		</dependency>
   		<!-- https://mvnrepository.com/artifact/com.googlecode.soundlibs/jlayer -->
   		<dependency>
   			<groupId>com.googlecode.soundlibs</groupId>
   			<artifactId>jlayer</artifactId>
   			<version>1.0.1-1</version>
   		</dependency>
   
   	</dependencies>
   	<build>
   		<plugins>
   			<plugin>
   				<groupId>org.codehaus.mojo</groupId>
   				<artifactId>exec-maven-plugin</artifactId>
   				<version>1.2.1</version>
   				<executions>
   					<execution>
   						<goals>
   							<goal>java</goal>
   						</goals>
   					</execution>
   				</executions>
   				<configuration>
   					<mainClass>com.amazonaws.demos.polly.PollyDemo</mainClass>
   				</configuration>
   			</plugin>
   		</plugins>
   	</build>
   </project>
   ```

1.  Create a new directory called `polly` at `src/main/java/com/amazonaws/demos`\. 

1.  In the `polly` directory, create a new Java source file called `PollyDemo.java`, and paste in the following code: 

   ```
   package com.amazonaws.demos.polly;
   
   import java.io.IOException;
   import java.io.InputStream;
   
   import com.amazonaws.ClientConfiguration;
   import com.amazonaws.auth.DefaultAWSCredentialsProviderChain;
   import com.amazonaws.regions.Region;
   import com.amazonaws.regions.Regions;
   import com.amazonaws.services.polly.AmazonPollyClient;
   import com.amazonaws.services.polly.model.DescribeVoicesRequest;
   import com.amazonaws.services.polly.model.DescribeVoicesResult;
   import com.amazonaws.services.polly.model.OutputFormat;
   import com.amazonaws.services.polly.model.SynthesizeSpeechRequest;
   import com.amazonaws.services.polly.model.SynthesizeSpeechResult;
   import com.amazonaws.services.polly.model.Voice;
   
   import javazoom.jl.player.advanced.AdvancedPlayer;
   import javazoom.jl.player.advanced.PlaybackEvent;
   import javazoom.jl.player.advanced.PlaybackListener;
   
   public class PollyDemo {
   
   	private final AmazonPollyClient polly;
   	private final Voice voice;
   	private static final String SAMPLE = "Congratulations. You have successfully built this working demo 
   	of Amazon Polly in Java. Have fun building voice enabled apps with Amazon Polly (that's me!), and always 
   	look at the AWS website for tips and tricks on using Amazon Polly and other great services from AWS";
   
   	public PollyDemo(Region region) {
   		// create an Amazon Polly client in a specific region
   		polly = new AmazonPollyClient(new DefaultAWSCredentialsProviderChain(), 
   		new ClientConfiguration());
   		polly.setRegion(region);
   		// Create describe voices request.
   		DescribeVoicesRequest describeVoicesRequest = new DescribeVoicesRequest();
   
   		// Synchronously ask Amazon Polly to describe available TTS voices.
   		DescribeVoicesResult describeVoicesResult = polly.describeVoices(describeVoicesRequest);
   		voice = describeVoicesResult.getVoices().get(0);
   	}
   
   	public InputStream synthesize(String text, OutputFormat format) throws IOException {
   		SynthesizeSpeechRequest synthReq = 
   		new SynthesizeSpeechRequest().withText(text).withVoiceId(voice.getId())
   				.withOutputFormat(format);
   		SynthesizeSpeechResult synthRes = polly.synthesizeSpeech(synthReq);
   
   		return synthRes.getAudioStream();
   	}
   
   	public static void main(String args[]) throws Exception {
   		//create the test class
   		PollyDemo helloWorld = new PollyDemo(Region.getRegion(Regions.US_EAST_1));
   		//get the audio stream
   		InputStream speechStream = helloWorld.synthesize(SAMPLE, OutputFormat.Mp3);
   
   		//create an MP3 player
   		AdvancedPlayer player = new AdvancedPlayer(speechStream,
   				javazoom.jl.player.FactoryRegistry.systemRegistry().createAudioDevice());
   
   		player.setPlayBackListener(new PlaybackListener() {
   			@Override
   			public void playbackStarted(PlaybackEvent evt) {
   				System.out.println("Playback started");
   				System.out.println(SAMPLE);
   			}
   			
   			@Override
   			public void playbackFinished(PlaybackEvent evt) {
   				System.out.println("Playback finished");
   			}
   		});
   		
   		
   		// play it!
   		player.play();
   		
   	}
   }
   ```

1.  Return to the `polly-java-demo` directory to clean, compile, and execute the demo: 

   ```
   mvn clean compile exec:java
   ```