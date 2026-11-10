# Looking Up Business Applications and Their Risk Rating

Business applications live in the CMDB table `cmdb_ci_business_app`. In many instances, each business application carries a **Primary App ID** that points to a record in a separate **Application Registry**, which holds the **Application Risk Rating**, owner, support group, and other details.

## Open the business application list

**Fast way:** in the filter navigator, type `cmdb_ci_business_app.list` and press **Enter**. Typing `.LIST` in capitals opens it in a new tab.

**Menu way:** type **Business Applications** in the filter navigator. It usually appears under **Configuration** or **Application Portfolio Management**.

If the list is empty or you get an access error, you likely need a CMDB read role such as `cmdb_read` or `itil`.

## Check how the Primary App ID is stored

1. Open any business application record.
2. Look at the **Primary App ID** field.
   - A small **(i)** icon or a clickable value means it is a **reference** field. Use Option A.
   - Plain text means it is a **string** field. Use Option B.

## Option A: Reference field (dot-walking)

**One application:** click the **(i)** icon to preview the registry record, risk rating included.

**Many applications:**

1. Open the business application list.
2. Click the **gear icon** at the top left of the list.
3. In **Available**, find **Primary App ID** and click its expand control.
4. Select **Application Risk Rating**, move it to **Selected**, and click **OK**.

Every row now shows its risk rating, and you can filter or group by it.

## Option B: String field (manual join)

### One application

1. Copy the **Primary App ID** from the business application.
2. Open the **Application Registry** list.
3. Paste the ID into the search box above the **App ID** column and press **Enter**.
4. Read the **Application Risk Rating**.

### A batch of applications ("is one of")

1. On the business application list, filter to the applications you need.
2. Add **Primary App ID** as a column if needed (gear icon).
3. Right click the column header, choose **Export > Excel**, and copy the IDs.
4. Open the **Application Registry** list and click the **funnel icon**.
5. Set the condition to **App ID** **is one of**.
6. Paste the IDs, one per line, and click **Run**.

### Everything (Excel join)

1. Export the business application list (Name and Primary App ID).
2. Export the Application Registry list (App ID, Application Risk Rating, and anything else you need) to a second sheet.
3. Use `XLOOKUP` on the ID to pull the rating onto each business application.

This works for a one time view but goes stale as ratings change.

## Also check the other direction

Open a registry record and look for a reference field or related list pointing back to the business application. If one exists, you can dot-walk from the registry side instead.

## Find a table's real name

1. Open the list.
2. Right click any column header and choose **Copy URL**, or look at the browser address bar.
3. The table name appears in the URL. Custom tables and fields often start with `u_` or a scoped prefix such as `x_company_`.

You can then jump straight to it by typing `<table_name>.list` in the filter navigator.

## Find a custom field anywhere

1. In the filter navigator, type `sys_dictionary.list` and press **Enter**.
2. Filter on **Column label** *contains* the field name (for example `Risk Rating`).
3. The **Table** column shows where the field lives.

## Longer term fix

If the risk rating will drive automation (incident priority, routing, integrations), a string link is fragile. Ask the platform team to convert **Primary App ID** to a reference field, or to build a **database view** joining the two tables on the ID. Until then, an integration needs two Table API calls: one to read the ID from the business application, and one to read the registry record.
