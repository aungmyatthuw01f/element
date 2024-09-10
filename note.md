### Logging into the Server Using Element

1. **Open Element Web**:
   - Navigate to the Element web interface hosted on your server (e.g., `http://tnclog.com` if you've set it up to be accessible via a domain or `http://localhost` if accessing locally).

2. **Login**:
   - Use the username and password you created during registration or the first admin user you set up. If you haven’t set up an admin user yet, you’ll initially log in with any user account you’ve created that can be granted admin privileges later.

### Setting Admin Privileges

If the account you are using does not have admin privileges, you can grant these via the database or a configuration script, depending on how your server is set up. Here's how to grant admin rights to a user directly in the database for a common Synapse setup:

1. **Access Your Server**:
   - SSH into your server where Synapse is running.

2. **Access the Database**:
   - If you are using SQLite (default setup), access the database with the following command:
     ```bash
     sqlite3 /path/to/homeserver.db
     ```
   - If using PostgreSQL, connect using:
     ```bash
     psql -h localhost -U synapse_user synapse
     ```

3. **Modify the User's Admin Status**:
   - Execute the following SQL command, replacing `@yourusername:tnclog.com` with the full Matrix ID of the user you want to grant admin rights to:
     ```sql
     UPDATE users SET admin = 1 WHERE name = '@yourusername:tnclog.com';
     ```

4. **Exit the Database**:
   - For SQLite:
     ```bash
     .quit
     ```
   - For PostgreSQL:
     ```bash
     \q
     ```

### Using the Admin API

Once you have admin rights, you can also use the Admin API provided by Synapse for more advanced management tasks. Access this through API clients like Postman, or directly via `curl` commands. For example, to retrieve information about a user:

```bash
curl -X GET -H "Authorization: Bearer YOUR_ACCESS_TOKEN" 'https://tnclog.com/_synapse/admin/v1/users/@username:tnclog.com'
```

Replace `YOUR_ACCESS_TOKEN` with your valid admin user access token.

### Accessing the Admin Console in Element

Element itself does not have a specialized "admin console," but you can perform various administrative tasks through it, such as managing rooms, users, and permissions. For deeper administrative functionalities like server configuration or user management, you would use the Synapse Admin API as mentioned above.

### Summary

To administer your Matrix Synapse server, you will primarily use a combination of:
- A Matrix client like Element for general user and room management.
- Direct database access for critical administrative actions.
- The Synapse Admin API for programmatically managing the server.
