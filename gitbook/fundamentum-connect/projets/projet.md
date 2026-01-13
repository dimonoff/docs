# Projet

This section allows you to configure and manage various aspects of the project through several tabs.\
Each tab supports precise and organized management of the project settings:

*   **Configuration:**

    * **Organization:** Allows you to change the name of the organization linked to the project.
    * **Billing:** Each project must be assigned a billing ID. This system allows customers to bill multiple projects to the same account or to allocate costs for different environments (e.g., staging, production) to separate billing accounts.
    * **Project ID:** A unique number associated with a project that identifies it in the database. It cannot be changed from this menu.
    * **ID:** A unique identifier used to access Fundamentum APIs.
    * **Email address for sending notifications:** Allows you to change the email address used to send notifications.
    * **Application URL:** Allows you to define the application URL.

    **Meta Data:** Enables customers to provide non-Fundamentum data to a project in JSON format.

    Click **Update Project** to save the changes.

<figure><img src="../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Roles**: Allows you to add new roles for project members in order to define their permissions and access.\
  ![](<../../.gitbook/assets/image (70).png>)

<figure><img src="../../.gitbook/assets/image (8) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (9) (1) (1).png" alt=""><figcaption></figcaption></figure>

Once you have created the role, you can see the actions that are securable for the containers containign your role, and sub-containers:<br>

<figure><img src="../../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

Edit permissions by clicking the Edit button at the end of the row of your action:

<figure><img src="../../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

Checking the “All” permission for an action unchecks and disables the “Own” permission, because they are mutually exclusive.

Checking permissions and saving will reflect the changes in the permissions grid:

<figure><img src="../../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>



* **Containers**: are logical units on which actions can be performed (and secured via permissions). Containers also contain other containers.

Platform admins can manage system containers, which can be used in any project. Project containers can only be used in that project.

These are the default containers included in Fundamentum:

<figure><img src="../../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

The default containers are system containers, they can only be modified by platform admins. Project admins can create their own containers, which other projects won’t see. This is done in the “Containers” tab of the project management screen:

<figure><img src="../../.gitbook/assets/image (10) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

Project containers have a prefix to their name to prevent collisions, this prefix cannot be changed.

Once you have created your container, you can manage actions on that container:

<figure><img src="../../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

Create an action by clicking the New Action button:

<figure><img src="../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

Name is the action name that can be validated when checking permission.

Scope determines if that permission is granted for all containers of that type (Global) or only the container for which the permission was granted (Personal).

Set an icon, a label and a description for your Action.

If you create the same action for both global and personal scopes, use the same action name but have different labels.

<figure><img src="../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

Later, you’ll be able to secure actions on this container:

<figure><img src="../../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>



* **License Types :**  are managed per-project, in the License Types tab of the project screen:

<figure><img src="../../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>

Create a new license type by clicking the New button:

<figure><img src="../../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

Once you have created your license type, you can add option fields to your license type:

<figure><img src="../../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

Add new option fields using the New button:

<figure><img src="../../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>

Name is the field name that will be available when querying license optionsa values for a license using that license type.

Label is displayed when editing this option’s value in a license.

Type is the value type to store. Text means any string of characters, Number means noly integer numbers, and True/False means a boolean value.

Default value is the default value to use for this option when creating new licenses of that license type, or for existing licenses is you are adding a new option.

Required indicates wether that this option must have a non-empty (or non-zero) value when saving a license of that license type.

Your options will be presented in the license edition screen:

<figure><img src="../../.gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>



* **Zone types** : are types that can be assigned to Zones

Platform Admins can create zone types that are available to all projects. Project managers can create zone types that are only usable in their project.

These are the default system zone types:

<figure><img src="../../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>

There are no default project zone types:

<figure><img src="../../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>

To create a platform-wide or project-scoped zone type (depending on where you are), click on the Create button:

<figure><img src="../../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>

