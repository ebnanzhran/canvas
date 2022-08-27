# DEFINITION OF ROLE-BASED ACCESS CONTROL (RBAC)

Role-based access control (RBAC) restricts network access based on a person's role within an organization and has become one of the main methods for advanced access control. The roles in RBAC refer to the levels of access that employees have to the network.

Employees are only allowed to access the information necessary to effectively perform their job duties. Access can be based on several factors, such as authority, responsibility, and job competency. In addition, access to computer resources can be limited to specific tasks such as the ability to view, create, or modify a file.

As a result, lower-level employees usually do not have access to sensitive data if they do not need it to fulfill their responsibilities. This is especially helpful if you have many employees and use third-parties and contractors that make it difficult to closely monitor network access. Using RBAC will help in securing your company’s sensitive data and important applications.

## EXAMPLES OF ROLE-BASED ACCESS CONTROL
Through RBAC, you can control what end-users can do at both broad and granular levels. You can designate whether the user is an administrator, a specialist user, or an end-user, and align roles and access permissions with your employees’ positions in the organization. Permissions are allocated only with enough access as needed for employees to do their jobs.

What if an end-user's job changes? You may need to manually assign their role to another user, or you can also assign roles to a role group or use a role assignment policy to add or remove members of a role group.

Some of the designations in an RBAC tool can include:

* Management role scope – it limits what objects the role group is allowed to manage.
* Management role group – you can add and remove members.
* Management role – these are the types of tasks that can be performed by a specific role group.
* Management role assignment – this links a role to a role group.

## BENEFITS OF RBAC
Managing and auditing network access is essential to information security. Access can and should be granted on a need-to-know basis. With hundreds or thousands of employees, security is more easily maintained by limiting unnecessary access to sensitive information based on each user’s established role within the organization. Other advantages include

# react-cookie

## Integrations
* universal-cookie - Universal cookies for JavaScript
* universal-cookie-express - Hook cookies get/set on Express for server-rendering

## Minimum requirement
### react-cookie @ v3.0+
* React.js >= 16.3.0 (new context API + forward ref)
### react-cookie @ v0.0-v2.2
* React.js >= 15

### npm install react-cookie

or in the browser (global variable ReactCookie):
```
<script
  crossorigin
  src="https://unpkg.com/react@16/umd/react.production.js"
></script>
<script
  crossorigin
  src="https://unpkg.com/universal-cookie@3/umd/universalCookie.min.js"
></script>
<script
  crossorigin
  src="https://unpkg.com/react-cookie@3/umd/reactCookie.min.js"
></script>
```

## <CookiesProvider />
Set the user cookies

On the server, the cookies props must be set using req.universalCookies or new Cookie(cookieHeader)

## useCookies([dependencies])
Access and modify cookies using React hooks.
```
const [cookies, setCookie, removeCookie] = useCookies(['cookie-name']);
```

## withCookies(Component)
Give access to your cookies anywhere. Add the following props to your component:

cookies: Cookies instance allowing you to get, set and remove cookies.
allCookies: All your current cookies in an object.
Your original static properties will be hoisted on the returned component. You can also access the original component by using the WrappedComponent static property. Example:
```
function MyComponent() {
  return null;
}
const NewComponent = withCookies(MyComponent);
NewComponent.WrappedComponent === MyComponent;
```