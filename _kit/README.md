# Content review kit

Lets reviewers without Claude accounts edit copy on a prototype and save it automatically.

- Hosting: this repo deploys to Vercel project `vd-review` (team p3rpl3xity-gmailcoms-projects) at https://vd-review.vercel.app/. Deployments are triggered with the Vercel connector (create_deployment, gitSource github P3RPL3XITY/vd-review ref main, target production).
- Storage: Supabase project "Visit Dubai" (jvpiloteofuvotnfoyho), table `public.copy_suggestions` (market = project name, page = page title without " · Visit Dubai prototype", path, original, text, author, device, withdrawn, status new/approved/applied/rejected). Anonymous insert + select only.
- `edit-copy.html` is the block to paste just before `</body>` of every page. Replace `__PROJECT__` with the project name (same for every page of that project) and `__REVIEW_PATH__` with that page's path on the review site (e.g. `museum/` or `museum/checkout.html`).
- The same pages go on the Claude link and in a folder here. On a Claude link the red Edit copy tab opens the review page (`?edit=1` opens edit mode). On the review site it saves to Supabase and shows saved suggestions to everyone.
- Applying: read rows with status 'new', latest per device+path, ignore withdrawn ones; apply the approved text to the source, republish the Claude link, copy the files here, push, deploy, then set status to 'applied' or 'rejected'.
