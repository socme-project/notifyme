# NOTIFYme

NOTIFYme is a simple golang library designed to send notifications via various channels such as email, Telegram, and ntfy.sh, also allowing you to send a message to multiple notification channels at once.

## Installation

To install NOTIFYme, you can use the following command:

```bash
go get github.com/socme-project/notifyme
```

## Usage

To use NOTIFYme, you need to import the package in your Go code:

```go
import "github.com/socme-project/notifyme"
```

You can then create a new notifier and send notifications through different channels. Here's a simple example:

```go
func main() {

  // Initialize the Telegram notifier with your ChatID and token
 tel := notifyme.Telegram(0, "teltoken")

 test, err := tel.HelperGetChatIds()
 if err != nil {
  fmt.Println(err)
 }

 chatid := test["hey"]
 if chatid == 0 {
  fmt.Println("ChatId not found")
 }

 notifiers := notifyme.Notifiers{tel}

 errs := notifiers.Notify("Test", "Hello World")
 if errs != nil {
  fmt.Println(errs)
 }

 fmt.Println("Notification sent successfully!")

 // Initialize the Email notifier
 email := notifyme.Email("alice@gmail.com", "password", "bob@gmail.com", "smtp.gmail.com", "587")
 err = email.Notify("Test Email", "Hello from NOTIFYme!")
 if err != nil {
  fmt.Println("Error sending email:", err)
 } else {
  fmt.Println("Email sent successfully!")
 }

 // Initialize the ntfy notifier
 ntfy := notifyme.Ntfy("http://localhost:8080", "topic")
 err = ntfy.Notify("Test Ntfy", "Hello from NOTIFYme!")

}
