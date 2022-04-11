# Get the IAM account password policy using an AWS SDK<a name="example_iam_GetAccountPasswordPolicy_section"></a>

The following code examples show how to get the IAM account password policy\.

**Note**  
The source code for these examples is in the [AWS Code Examples GitHub repository](https://github.com/awsdocs/aws-doc-sdk-examples)\. Have feedback on a code example? [Create an Issue](https://github.com/awsdocs/aws-doc-sdk-examples/issues/new/choose) in the code examples repo\. 

------
#### [ Go ]

**SDK for Go V2**  
  

```
	// GetAccountPasswordPolicy

	fmt.Println("🔐 GetAccountPasswordPolicy")

	accountPasswordPolicy, err := service.GetAccountPasswordPolicy(context.Background(), &iam.GetAccountPasswordPolicyInput{})

	if err != nil {
		var notexists *types.NoSuchEntityException
		if errors.As(err, &notexists) {
			fmt.Println("No password policy")
		} else {
			panic("Couldn't get account password policy! " + err.Error())
		}
	} else {
		fmt.Println("Users can change password: ", accountPasswordPolicy.PasswordPolicy.AllowUsersToChangePassword)
		fmt.Println("Passwords expire: ", accountPasswordPolicy.PasswordPolicy.ExpirePasswords)
		fmt.Println("Minimum password length: ", accountPasswordPolicy.PasswordPolicy.MinimumPasswordLength)
	}
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/gov2/iam#code-examples)\. 
+  For API details, see [GetAccountPasswordPolicy](https://pkg.go.dev/github.com/aws/aws-sdk-go-v2/service/iam#Client.GetAccountPasswordPolicy) in *AWS SDK for Go API Reference*\. 

------
#### [ JavaScript ]

**SDK for JavaScript V3**  
Create the client\.  

```
import { IAMClient } from "@aws-sdk/client-iam";
// Set the AWS Region.
const REGION = "REGION"; // For example, "us-east-1".
// Create an IAM service client object.
const iamClient = new IAMClient({ region: REGION });
export { iamClient };
```
Get the account password policy\.  

```
// Import required AWS SDK clients and commands for Node.js.
import { iamClient } from "./libs/iamClient.js";
import { GetAccountPasswordPolicyCommand } from "@aws-sdk/client-iam";

const run = async () => {
  try {
    const data = await iamClient.send(new GetAccountPasswordPolicyCommand({}));
    console.log("Success", data.PasswordPolicy);
  } catch (err) {
    console.log("Error", err);
  }
};
run();
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/javascriptv3/example_code/iam#code-examples)\. 
+  For API details, see [GetAccountPasswordPolicy](https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/clients/client-iam/classes/getaccountpasswordpolicycommand.html) in *AWS SDK for JavaScript API Reference*\. 

------
#### [ PHP ]

**SDK for PHP**  
  

```
$uuid = uniqid();
$service = new IamService();

    public function getAccountPasswordPolicy()
    {
        return $this->iamClient->getAccountPasswordPolicy();
    }
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/php/example_code/iam/iam_basics#code-examples)\. 
+  For API details, see [GetAccountPasswordPolicy](https://docs.aws.amazon.com/goto/SdkForPHPV3/iam-2010-05-08/GetAccountPasswordPolicy) in *AWS SDK for PHP API Reference*\. 

------
#### [ Python ]

**SDK for Python \(Boto3\)**  
  

```
def print_password_policy():
    """
    Prints the password policy for the account.
    """
    try:
        pw_policy = iam.AccountPasswordPolicy()
        print("Current account password policy:")
        print(f"\tallow_users_to_change_password: {pw_policy.allow_users_to_change_password}")
        print(f"\texpire_passwords: {pw_policy.expire_passwords}")
        print(f"\thard_expiry: {pw_policy.hard_expiry}")
        print(f"\tmax_password_age: {pw_policy.max_password_age}")
        print(f"\tminimum_password_length: {pw_policy.minimum_password_length}")
        print(f"\tpassword_reuse_prevention: {pw_policy.password_reuse_prevention}")
        print(f"\trequire_lowercase_characters: {pw_policy.require_lowercase_characters}")
        print(f"\trequire_numbers: {pw_policy.require_numbers}")
        print(f"\trequire_symbols: {pw_policy.require_symbols}")
        print(f"\trequire_uppercase_characters: {pw_policy.require_uppercase_characters}")
        printed = True
    except ClientError as error:
        if error.response['Error']['Code'] == 'NoSuchEntity':
            print("The account does not have a password policy set.")
        else:
            logger.exception("Couldn't get account password policy.")
            raise
    else:
        return printed
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/python/example_code/iam/iam_basics#code-examples)\. 
+  For API details, see [GetAccountPasswordPolicy](https://docs.aws.amazon.com/goto/boto3/iam-2010-05-08/GetAccountPasswordPolicy) in *AWS SDK for Python \(Boto3\) API Reference*\. 

------
#### [ Ruby ]

**SDK for Ruby**  
  

```
  # Prints the password policy for the account.
  def print_account_password_policy
    policy = @iam_resource.account_password_policy
    policy.load
    puts("The account password policy is:")
    puts(policy.data.to_h)
  rescue Aws::Errors::ServiceError => e
    if e.code == "NoSuchEntity"
      puts("The account does not have a password policy.")
    else
      puts("Couldn't print the account password policy. Here's why:")
      puts("\t#{e.code}: #{e.message}")
      raise
    end
  end
```
+  Find instructions and more code on [GitHub](https://github.com/awsdocs/aws-doc-sdk-examples/tree/main/ruby/example_code/iam#code-examples)\. 
+  For API details, see [GetAccountPasswordPolicy](https://docs.aws.amazon.com/goto/SdkForRubyV3/iam-2010-05-08/GetAccountPasswordPolicy) in *AWS SDK for Ruby API Reference*\. 

------

For a complete list of AWS SDK developer guides and code examples, see [Using IAM with an AWS SDK](sdk-general-information-section.md)\. This topic also includes information about getting started and details about previous SDK versions\.