jenkinsc

# Update package index
sudo apt update

# Install Java and fontconfig
sudo apt install fontconfig openjdk-21-jdk -y

# Create Jenkins keyring directory
sudo mkdir -p /etc/apt/keyrings

# Download Jenkins key
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key

# Add Jenkins repository
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

# Update package index
sudo apt update

# Install Jenkins
sudo apt-get install jenkins -y

# Configure Java version
sudo update-alternatives --config java

# Start Jenkins
sudo systemctl start jenkins

# Enable Jenkins
sudo systemctl enable jenkins

# Check Jenkins status
sudo systemctl status jenkins

# Get initial Jenkins administrator password
sudo cat /var/lib/jenkins/secrets/initialAdminPassword

After installation, open http://localhost:8080 and complete the Jenkins initial setup.

Yes! Here are all four Jenkins pipelines using direct Java files (without Maven) with three stages: Checkout, Build and Execute.

1. Palindrome
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/YOUR_USERNAME/Palindrome-Jenkins-CI.git'
            }
        }

        stage('Build') {
            steps {
                sh 'javac Palindrome.java'
            }
        }

        stage('Execute') {
            steps {
                sh 'echo 121 | java Palindrome'
            }
        }
    }
}
Expected output: Palindrome Number

2. Prime Number
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/YOUR_USERNAME/Prime-Jenkins-CI.git'
            }
        }

        stage('Build') {
            steps {
                sh 'javac Prime.java'
            }
        }

        stage('Execute') {
            steps {
                sh 'echo 7 | java Prime'
            }
        }
    }
}
Expected output: Prime Number

3. Factorial
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/YOUR_USERNAME/Factorial-Jenkins-CI.git'
            }
        }

        stage('Build') {
            steps {
                sh 'javac Factorial.java'
            }
        }

        stage('Execute') {
            steps {
                sh 'echo 5 | java Factorial'
            }
        }
    }
}
Expected output: Factorial = 120

4. Fibonacci
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/YOUR_USERNAME/Fibonacci-Jenkins-CI.git'
            }
        }

        stage('Build') {
            steps {
                sh 'javac Fibonacci.java'
            }
        }

        stage('Execute') {
            steps {
                sh 'echo 7 | java Fibonacci'
            }
        }
    }
}
Expected output: 0 1 1 2 3 5 8

Common procedure
Upload the .java file to GitHub.
Open Jenkins.
Click New Item → Pipeline.
Enter the job name.
Select Pipeline script.
Paste the respective code.
Click Apply → Save.
Click Build Now.
Open Console Output.
Remember these three commands:

Stage	Command	Purpose
Checkout	git	Download code
Build	javac Filename.java	Compile code
Execute	echo input \| java ClassName	Run code
Same three-stage structure for all four programs

Just replace YOUR_USERNAME with your GitHub username before running.

Here are all four Java programs for your Jenkins CI experiments. These use Scanner, loops and simple logic, without Maven.

1. Palindrome Number
File name: Palindrome.java

import java.util.Scanner;

public class Palindrome {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter a number: ");
        int num = sc.nextInt();

        int original = num;
        int reverse = 0;

        while (num > 0) {
            int digit = num % 10;
            reverse = reverse * 10 + digit;
            num = num / 10;
        }

        if (original >= 0 && original == reverse) {
            System.out.println("Palindrome Number");
        } else {
            System.out.println("Not a Palindrome Number");
        }

        sc.close();
    }
}
Output:

Enter a number: 121
Palindrome Number
2. Prime Number
File name: Prime.java

import java.util.Scanner;

public class Prime {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter a number: ");
        int num = sc.nextInt();

        boolean prime = true;

        if (num <= 1) {
            prime = false;
        } else {
            for (int i = 2; i <= num / 2; i++) {
                if (num % i == 0) {
                    prime = false;
                    break;
                }
            }
        }

        if (prime) {
            System.out.println("Prime Number");
        } else {
            System.out.println("Not a Prime Number");
        }

        sc.close();
    }
}
Output:

Enter a number: 7
Prime Number
3. Factorial
File name: Factorial.java

import java.util.Scanner;

public class Factorial {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter a number: ");
        int num = sc.nextInt();

        long fact = 1;

        for (int i = 1; i <= num; i++) {
            fact = fact * i;
        }

        System.out.println("Factorial = " + fact);

        sc.close();
    }
}
Output:

Enter a number: 5
Factorial = 120
4. Fibonacci Series
File name: Fibonacci.java

import java.util.Scanner;

public class Fibonacci {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter the number of terms: ");
        int n = sc.nextInt();

        int a = 0, b = 1;

        System.out.println("Fibonacci Series:");

        for (int i = 1; i <= n; i++) {
            System.out.print(a + " ");

            int c = a + b;
            a = b;
            b = c;
        }

        sc.close();
    }
}
Output:

Enter the number of terms: 7
Fibonacci Series:
0 1 1 2 3 5 8
Important: Commands for Jenkins
Use these commands in the respective pipeline stages.

Program	Build command	Execute command
Palindrome	javac Palindrome.java	echo 121 \| java Palindrome
Prime	javac Prime.java	echo 7 \| java Prime
Factorial	javac Factorial.java	echo 5 \| java Factorial
Fibonacci	javac Fibonacci.java	echo 7 \| java Fibonacci
Remember: The Java filename and public class name must match exactly. Upload each .java file to its corresponding GitHub repository.
