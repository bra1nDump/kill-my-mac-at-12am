# kill my mac and let me sleep
- I want to got to bed at a consistent time for health, productivity, and social reasons
- When I don't go to bed early, chances are I am coding / watching something on my mac
- The system suggestions to 'go to bed' are too easy to ignore, I tune them out magically

## How it works
- If computer is not asleep or shut down when sleep hours start - it will be shut down
- Sleep hours currently are hardcoded: 12am - 6am, open an issue if you want to see them customized
- 1 hour and 10 minutes before the sleep hours start the computer will warn you, if your sound is on

## How to install:
In your terminal run

```bash
# Clone the repo
git clone https://github.com/bra1nDump/kill-my-mac.git
cd kill-my-mac

# So you can run kill-my-mac from anywhere on your computer
ln -sf kill-my-mac.sh /usr/local/bin/kill-my-mac

# Run this to configure the app
kill-my-mac
```

## How does it actually work?
- It installs a [LaunchAgent](./templates/com.bra1ndump.shutdown-during-sleep-hours.plist) that runs shutdown-job every minute
  - You can find the agent configuration here `ls ~/Library/LaunchAgents`
- [shutdown-job.sh](./shutdown-job.sh)
  - If computer is already asleep (uses `pmset`), do nothing
  - If close to sleep hours, warns the user
  - If in sleep hours, shut down using apple script `osascript -e 'tell application "System Events" to shut down'`

# TODO:

- Post about it
- TELL MY FRIENDS TO TRY IT

# Later:
- Package with Homebrew tap
- Allow configuring sleep time

- [better onboarding / configuration experience]
- Once installed do the setup with
  - Run `sleep-by`
  - Prompted:
    - Choose a time when you want to ensure your computer is not running
    - Format is: 00:20-06:00, no spaces, period start, period end, 24 hr format
    - In this example starting at 20 past midnight until 6, if your computer is not asleep, it will be forcefully shut down
  - Enter the time - default is 00:00-06:00 (midnight until 6am): Get

- How can I make editing the configuration difficult?
- By allowing to skip the shutdown once by looking at a message to self you wrote when setting this up, and forcing to look at it for 5 minutes before allowing to skip
- Maybe switch to python? Since it will be installed by brew, I can just set python as a dependency. Its installed everywhere already so does not really matter. Bash is fucking ridiculous. Functions are unlike in any other programming language

# Alternatives:
- Work on the discipline in other ways
- `pmset repeat shutdown TWRFS 11:00:00`
- Almighty https://indiegoodies.com/almighty - many different shortcuts
