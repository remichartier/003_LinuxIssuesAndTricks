# Edge Browser on Linux : Impossible to add work profile.md

Sources : 
- https://techcommunity.microsoft.com/t5/discussions/how-to-setup-a-work-profile-on-edge-dev-channel-on-linux-ubuntu/m-p/2305837
- https://techcommunity.microsoft.com/t5/articles/users-can-now-sign-in-and-sync-their-favorites-with-microsoft/m-p/2230134/page/3
- https://techcommunity.microsoft.com/t5/discussions/azure-ad-sign-in-support-in-edge-for-linux/m-p/2555908

Abbreviations / Acronyms : 
- Azure Active Directory (Azure AD)

Problem : 

- On Windows 10, Edge browser is able to define a work profile and activate data sync so that login in this work provile on any other computer triggers the sync of favorites on this destination browser so that we do not need to export/import them manually
- On Linux/Ubuntu, Edge browser is not accepting work account signin (like firstname.lastname@company.com) while adding an Edge profile. Doing a "sign-in to sync data" and specifying a work account leads to error message : 

`We couldn't find an account with that email address or phone number. Would you like to sign up for a new Microsoft account? Sign up`
