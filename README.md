                } // END ADMIN LOOP
            }

            // ================= CREDITOR =================
           else if (mainChoice.equals("2")) {
                System.out.print("====== CREDITOR LOGIN ====== ");
                System.out.print("Enter ID: ");
                String id = sc.nextLine();

                boolean foundUser = false;

                for (int i = 0; i < count; i++) {
                    if (ids[i].equalsIgnoreCase(id) && !archived[i]) {

                        foundUser = true;

                        System.out.print("Enter Password (Contact #): ");
                        String pass = sc.nextLine();

                        if (contact[i].equals(pass)) {

                            int userChoice = 0;

                            while (userChoice != 3) {

                                System.out.println("\n======= CREDITOR DASHBOARD =======");
                                System.out.println("[1] View My Utang Record");
                                System.out.println("[2] Check Status");
                                System.out.println("[3] Logout");
                                System.out.print("Choose an option: ");

                                String input = sc.nextLine();
                                if (!input.matches("^[1-3]$")) {
                                    System.out.println("Invalid choice.");
                                    continue;
                                }

                                userChoice = Integer.parseInt(input);

                                // ================= VIEW RECORD =================
                                if (userChoice == 1) {

                                    System.out.println("\n==== MY UTANG RECORDS ====");

                                    for (int j = 0; j < count; j++) {
                                        if (ids[j].equalsIgnoreCase(id) && !archived[j]) {

                                            System.out.println("\nItem Summary: " + items[j]);
                                            System.out.println("Balance: " + balance[j]);
                                            System.out.println("Date of Credit: " + borrowed[j]);
                                            System.out.println("Due: " + due[j]);

                                            System.out.println("Item Breakdown:");
                                            String[] itemList = items[j].split(", ");
                                            for (String line : itemList) {
                                                if (!line.isEmpty()) {
                                                    System.out.println(" - " + line);
                                                }
                                            }
                                        }
                                    }
                                }

                                // ================= STATUS =================
                                else if (userChoice == 2) {

                                    LocalDate today = LocalDate.now();

                                    System.out.println("\n==== MY UTANG STATUS ====");

                                    for (int j = 0; j < count; j++) {
                                        if (ids[j].equalsIgnoreCase(id) && !archived[j]) {

                                            if (balance[j] == 0) {
                                                System.out.println("STATUS: PAID");
                                            }

                                            else if (balance[j] < totalAmount[j] && balance[j] > 0) {
                                                if (today.isAfter(due[j])) {
                                                    System.out.println("STATUS: PARTIALLY PAID (OVERDUE)");
                                                    System.out.println("WARNING: YOU STILL HAVE PARTIAL PAYMENT OVERDUE!");
                                                } else {
                                                    System.out.println("STATUS: PARTIALLY PAID");
                                                    System.out.println("REMINDER: YOU STILL HAVE PARTIAL PAYMENT DUE!");
                                                }
                                            }

                                            else if (today.isAfter(due[j])) {
                                                System.out.println("STATUS: OVERDUE");
                                                System.out.println("WARNING: YOUR UTANG IS OVERDUE!");
                                            }

                                            else {
                                                System.out.println("STATUS: UNPAID");
                                                System.out.println("REMINDER: YOUR UTANG IS NOT YET DUE");
                                            }
                                        }
                                    }
                                }

                        // ================= LOGOUT =================
                        else if (userChoice == 3) {
                            System.out.println("Logged Out!");
                        }
                    }

                } else {
                    System.out.println("Wrong password!");
                }

                break; 
            }
        }

        if (!foundUser) {
            System.out.println("Creditor not found.");
        }
    }

            // ================= EXIT =================
            else if (mainChoice.equals("3")) {
                System.out.println("Exiting Program....");
                break;
            }

            else {
                System.out.println("Invalid choice.");
            }
        }

        sc.close();
    }
}
   
