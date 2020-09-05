1)

Dear Customer,

In order to remove unwanted/benign errors from appearing in your Sentry.IO account you simply need to move the script tag where you include the libary. Specifically, the library needs to be included before/above the sentry.init function is called. Any libraries that are included before this function is invoked will not be captured by Sentry. Additionaly, there are some filtering options available with your Sentry dashboard that can help you filter out unwanted errors(https://docs.sentry.io/platforms/javascript/configuration/filtering/). I hope this helps!

Sincerely,
Hayden

Before: Orignally you included your library after Sentry.init was called.
<script>
Sentry.init({
  dsn: 'DSN_URL',
  release: "1.1"
});
</script>
<script src="https://somejslibrary.com/somelibrary.js" crossorigin="anonymous"></script>

After: For your use case just move the library up above the Sentry.init function.

<script src="https://somejslibrary.com/somelibrary.js" crossorigin="anonymous"></script>
<script>
Sentry.init({
  dsn: 'DSN_URL',
  release: "1.1"
});
</script>

Testing: I tested this with the Jquery library from Google using their CDN as the source for the library. I intentionally commented out the library and then called JQuery both before and after sentry.init was called. Everytime it was included after sentry.init it would generate an error($ is not defined) in my Sentry Dashboard. When I included the libary before and revisted the site multiple times it never showed/captured the error because it was invoked before Sentry could capture it. Below is the full file I was using for testing.

<!DOCTYPE html>
<html>
<head>
<title>Random Title</title>
<script
  src="https://browser.sentry-cdn.com/5.22.3/bundle.tracing.min.js"
  crossorigin="anonymous"
></script>
<script>
  $(document).ready(function(){
      $("p").text("JQuery working");
  });
</script>
<script>
Sentry.init({
  dsn: 'https://af2f66e4498246b18066c4cd2b65e9c8@o442880.ingest.sentry.io/5415907',
  release: "1.1"
});
</script>
<script src="https://somejslibrary.com/somelibrary.js" crossorigin="anonymous"></script>
<!--
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>

<script>
  $(document).ready(function(){
      $("p").text("JQuery working");
  });
</script>
-->

<script>
let obj={};
//obj.invalidFunction();
</script>
<body>
  <p>Jquery not working</p>
</body>

</head>
</html>

2) Dear Customer,

We offer multi tenant as the default option for most of our customers. And as you pointed out we do have a single tenant option avaiable as well. It is mentioned here(https://sentry.io/security) in our security docs. Since security is paramount for your company I would suggest setting up your instance under a single tenant. That was your information is fully secure and isolated at rest. Let me know if you have addiotnally questions about our security. I am more than happy to reach out to our security and engineering teams for any additional information or context needed.

Sincerely,
Hayden

3) Dear Customer,

It is possible to to only be alerted once a unique error happens 10 times within an hour timeframe. In order to do this you will need to modify your alert rules, here is an awesome article to reference later(https://sentry.io/resources/alert-rules/). Once you login into your Sentry dashboar click Alerts in the column on the left handside of the screen. Then click the purple create alert rule button in the top. Then select the project you want to create this custom alert for. Select your enviroment and then name the alert. Then in the drop down menu next to WHEN The issue is seen more than {value} times in {interval}. Simple put 10 for value and 60 minutes for interval. Then under THEN select send email. Then click create alert rule in the bottom right and your done. I hope this helps!

Sincerely
Hayden

4)
