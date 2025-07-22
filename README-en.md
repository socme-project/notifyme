# NOTIFYme

NOTIFYme is a simple golang library designed to send notifications via various
channels such as email, ntfy.sh, etc, also allowing you to send a message to
multiple notification channels at once.

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

You can then create a new notifier and send notifications through different
channels. Here's a simple example:

```go
func main() {
    // TELEGRAM
     chats, err := tel.HelperGetChatIds()
     if err != nil {
      fmt.Println(err)
     }

     chatid := chats["myUsername"]
     if chatid == 0 {
      fmt.Println("ChatId not found")
     }

      // Initialize the Telegram notifier with your ChatID and token
     tel := notifyme.Telegram(chatid, "telegram_token")

     notifiers := notifyme.Notifiers{tel}

     errs := notifiers.Notify("My title", "hello world! This is my notification message")
     if errs != nil {
      fmt.Println(errs)
     }

     fmt.Println("Notification sent successfully!")

     // Initialize the Email notifier
     email := notifyme.Email("fromEmail@gmail.com", "password", "toEmail@gmail.com", "smtp.gmail.com", "587")
     err = email.Notify("My title", "Hello from NOTIFYme!")
     if err != nil {
      fmt.Println("Error sending email:", err)
     }

     // Initialize the ntfy notifier
     ntfy := notifyme.Ntfy("http://localhost:8080", "topic")
     _ = ntfy.Notify("My title", "Hello from NOTIFYme!")
}
```
