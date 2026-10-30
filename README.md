# Bakery Project ERP

Website copy of the Bakery Project ERP (orders, bake sheets, purchasing, inventory, recipes and CG02-style specifications).

- The page is protected with an access code. Its content is encrypted (AES-256-GCM, key derived from the code with PBKDF2), so nothing is readable without the code.
- Records start from a snapshot of the ERP in Claude and are saved in each visitor's browser. Use **Setup › Export / Import** to move records between browsers or back into the Claude artifact.
- Asking questions in Query needs the Claude version; search works here.
