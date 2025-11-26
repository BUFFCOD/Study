
Use ps -u username to see only that user's processes.

use pkill -u username to send signals to all processes owned by that user.

loginctl can be used to manage user sessions. it is part of systemd.

one user can have mulitple sessions open simultaneously.

loginctl list-users and loginctl list-sessions can be used to view users and sessions.

loginctl user-status username or loginctl session-status sessionID can be used to view details about a user or session.

loginctl terminate-user username or loginctl terminate-session sessionID can be used to terminate all processes for a user or session.