//Name=Abdirahmaan mohamed Abdullahi
//ID=C6230254
//Class=CNS233

import java.util.Scanner;
import java.util.ArrayList;

// Class-ka ugu weyn
public class Abdirahmaan {

    // Variables static ah oo lagu kaydiyo lacagaha iyo PIN-yada
    static double haraaga = 100;         // Haraaga EVCPlus
    static double haraaga_bank = 400;    // Haraaga bangiga Salaam Bank
    static final int PIN = 1212;         // PIN-ka EVCPlus
    static final int BANK_PIN = 439891;  // PIN-ka bangiga (lama isticmaalin)
    static final String DIAL_CODE = "*770#"; // Lambar laga furo adeegga

    // Lists loogu talagalay in lagu kaydiyo taariikhda adeegyada
    static ArrayList<String> taariikhda = new ArrayList<>();       // Taariikhda guud
    static ArrayList<String> taajTaariikhda = new ArrayList<>();   // Taariikhda adeegga Taaj

    // Main method: halka barnaamijka ka bilaabmayo
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in); // Scanner si loo akhriyo input

        System.out.println("Dial Up");
        String dialUp = input.nextLine(); // Akhri lambarka laga furo

        // Haddii lambarka fure uu khaldan yahay
        if (!dialUp.equals(DIAL_CODE)) {
            System.out.println("Dhibaato xiriir ama lambar khaldan");
            return;
        }

        // Xaqiiji PIN
        System.out.println("-EVCPLUS-");
        System.out.println("Fadlan geli PIN-kaaga (Gali PIN)");
        int enteredPin = input.nextInt();

        // Haddii PIN-ka khaldan yahay
        if (enteredPin != PIN) {
            System.out.println("PIN-kaagu waa qalad");
            return;
        }

        // Loop-ka ugu weyn ee menu-ga adeegyada
        while (true) {
            displayMainMenu(input); // Soo bandhig menu-ga adeegyada

            // Weydiin isticmaalaha inuu sii wado
            System.out.println("\nMa rabtaa inaad sii waddo? (1 = Haa, 0 = Maya)");
            int cont = input.nextInt();
            if (cont != 1) {
                System.out.println("Waad ku mahadsantahay isticmaalka EVCPlus.");
                break; // Ka bax loop-ka
            }
        }
    }

    // Soo bandhig menu-ga adeegyada ugu waaweyn
    static void displayMainMenu(Scanner input) {
        System.out.println("\n--- EVCPlus ---");
        System.out.println("1. Itus Haraagaaga\n2. Kaarka hadalka\n3. Bixi Biil\n4. U wareeji EVCPlus\n5. Warbixin Kooban" +
                "\n6. Salaama Bank\n7. Maareynta\n8. Bill Payment\n9. Taaj Adeeg");

        int choice = input.nextInt(); // Doorashada isticmaalaha

        switch (choice) {
            case 1: displayBalance(); break;                 // Haraaga tus
            case 2: handleAirtimeMenu(input); break;         // U shub kaarka hadalka
            case 3: handleBillPayment(input); break;         // Biil bixi
            case 4: handleTransfer(input); break;            // U wareeji lacag
            case 5: taariikhdaMacmiilka(); break;            // Warbixin kooban
            case 6: handleBankMenu(input); break;            // Salaam Bank
            case 7: handleManagementMenu(input); break;      // Maareynta
            case 8: handleBillPaymentMenu(input); break;     // Bill Payment
            case 9: taajAdeeg(input); break;                 // Adeegga TAAJ
            default: System.out.println("Doorasho khaldan"); // Haddii doorashada khaldan tahay
        }
    }

    // Tus haraaga EVC
    static void displayBalance() {
        System.out.println("Haraagaaga waa: $" + haraaga);
        updateTaariikhda("Haraaga la fiiriyay: $" + haraaga);
    }

    // U shub kaarka hadalka
    static void handleAirtimeMenu(Scanner input) {
        System.out.println("Fadlan Geli Numberka aad u shubeyso:");
        String number = input.next();
        System.out.println("Fadlan Geli lacagta aad rabto in aad ku shubto:");
        double amount = input.nextDouble();

        if (amount <= haraaga) {
            haraaga -= amount;
            String msg = "$" + amount + " ayaa lagu shubay " + number;
            System.out.println(msg);
            updateTaariikhda(msg);
        } else {
            System.out.println("Haraagaaga kuguma filna");
        }
    }

    // Bixinta biil shirkadood
    static void handleBillPayment(Scanner input) {
        System.out.println("Fadlan Geli magaca shirkadda:");
        String company = input.next();
        System.out.println("Fadlan Geli lacagta biilka:");
        double amount = input.nextDouble();

        if (amount <= haraaga) {
            haraaga -= amount;
            String msg = "Waxaad bixisay $" + amount + " shirkadda " + company;
            System.out.println(msg);
            updateTaariikhda(msg);
        } else {
            System.out.println("Haraagaaga kuguma filna");
        }
    }

    // U wareeji EVCPlus
    static void handleTransfer(Scanner input) {
        System.out.println("Fadlan Geli numberka aad u wareejineyso:");
        String number = input.next();
        System.out.println("Fadlan Geli lacagta aad wareejineyso:");
        double amount = input.nextDouble();

        if (amount <= haraaga) {
            haraaga -= amount;
            String msg = "$" + amount + " ayaa loo wareejiyay " + number;
            System.out.println(msg);
            updateTaariikhda(msg);
        } else {
            System.out.println("Haraagaaga kuguma filna");
        }
    }

    // Salaam Bank: wareejin labada jiho
    static void handleBankMenu(Scanner input) {
        System.out.println("Salaam Bank\n1. Ka wareeji EVC → Bank\n2. Ka wareeji Bank → EVC");
        int doorasho = input.nextInt();

        switch (doorasho) {
            case 1:
                System.out.println("Lacagta aad rabto in aad u wareejiso Bankiga:");
                double evcToBank = input.nextDouble();
                if (evcToBank <= haraaga) {
                    haraaga -= evcToBank;
                    haraaga_bank += evcToBank;
                    String msg = "$" + evcToBank + " ayaa loo wareejiyay Salaam Bank";
                    System.out.println(msg);
                    updateTaariikhda(msg);
                } else {
                    System.out.println("Haraagaaga EVC kuma filna");
                }
                break;
            case 2:
                System.out.println("Lacagta aad rabto in aad kasoo saarto Bank → EVC:");
                double bankToEvc = input.nextDouble();
                if (bankToEvc <= haraaga_bank) {
                    haraaga_bank -= bankToEvc;
                    haraaga += bankToEvc;
                    String msg = "$" + bankToEvc + " ayaa laga soo wareejiyay Salaam Bank";
                    System.out.println(msg);
                    updateTaariikhda(msg);
                } else {
                    System.out.println("Haraaga Bankiga kuma filna");
                }
                break;
            default:
                System.out.println("Doorasho khaldan");
        }
    }

    // Menu-ga maareynta: bedel PIN ama eeg bank balance
    static void handleManagementMenu(Scanner input) {
        System.out.println("Maareynta\n1. Bedel PIN\n2. Eeg Haraaga Bangiga");
        int doorasho = input.nextInt();

        switch (doorasho) {
            case 1:
                System.out.println("Fadlan geli PIN-ka hadda:");
                int oldPin = input.nextInt();
                if (oldPin == PIN) {
                    System.out.println("Geli PIN cusub:");
                    int newPin = input.nextInt();
                    System.out.println("PIN cusub waa: " + newPin + " (Tijaabo ahaan, lama kaydin)");
                    updateTaariikhda("PIN ayaa la bedelay (muujin maaha)");
                } else {
                    System.out.println("PIN hore waa qalad");
                }
                break;
            case 2:
                System.out.println("Haraagaaga Salaam Bank waa: $" + haraaga_bank);
                updateTaariikhda("Eegid haraaga bangiga: $" + haraaga_bank);
                break;
            default:
                System.out.println("Doorasho khaldan");
        }
    }

    // Bixinta biil shirkado gaar ah
    static void handleBillPaymentMenu(Scanner input) {
        System.out.println("Dooro shirkadda aad biil u bixinayso:");
        System.out.println("1. SomPower\n2. Wadaagsan ISP\n3. EVC Utility");
        int doorasho = input.nextInt();
        String company = "";

        switch (doorasho) {
            case 1: company = "SomPower"; break;
            case 2: company = "Wadaagsan ISP"; break;
            case 3: company = "EVC Utility"; break;
            default:
                System.out.println("Doorasho aan sax ahayn");
                return;
        }

        System.out.println("Geli lacagta biilka:");
        double amount = input.nextDouble();

        if (amount <= haraaga) {
            haraaga -= amount;
            String msg = "Biil $" + amount + " ayaa laga bixiyay " + company;
            System.out.println(msg);
            updateTaariikhda(msg);
        } else {
            System.out.println("Haraaga EVC kuma filna");
        }
    }

    // Adeegga TAAJ: dir, hel, taariikh
    static void taajAdeeg(Scanner input) {
        System.out.println("[-EVCPlus-] TAAJ ADEEG");
        System.out.println("1. Dir Lacag\n2. Hel Lacag\n3. Warbixin Taariikheed");
        int choice = input.nextInt();

        switch (choice) {
            case 1:
                System.out.println("Fadlan Geli Mobile-ka Taaj");
                String number = input.next();
                System.out.println("Fadlan Geli Lacagta");
                double amount = input.nextDouble();
                if (amount <= haraaga) {
                    haraaga -= amount;
                    String msg = "$" + amount + " ayaad u dirtay Taaj: " + number;
                    System.out.println(msg);
                    updateTaariikhda(msg);
                    taajTaariikhda.add(msg);
                } else {
                    System.out.println("Haraagaaga kuguma filna");
                }
                break;
            case 2:
                System.out.println("Waxaad heshay lacag cusub. Mahadsanid.");
                taajTaariikhda.add("Lacag ayaad heshay - fariin tijaabo ah");
                break;
            case 3:
                System.out.println("Taariikhda macaamiisha Taaj:");
                if (taajTaariikhda.isEmpty()) {
                    System.out.println("Taariikh lama helin");
                } else {
                    for (int i = 0; i < taajTaariikhda.size(); i++) {
                        System.out.println((i + 1) + ". " + taajTaariikhda.get(i));
                    }
                }
                break;
            default:
                System.out.println("Doorasho khaldan");
        }
    }

    // Ku dar waxqabad cusub taariikhda
    static void updateTaariikhda(String msg) {
        taariikhda.add(0, msg); // Ku dar bilowga
        if (taariikhda.size() > 3) {
            taariikhda.remove(3); // Ka saar kii ugu dambeeyay (xadka waa 3)
        }
    }

    // Soo bandhig waxqabadka isticmaalaha
    static void taariikhdaMacmiilka() {
        System.out.println("[-EVCPlus-] Udambeeya waa 6$ waxaa uwareejisay 613291522:");
        if (taariikhda.isEmpty()) {
            // System.out.println("Ma jiro waxqabad hore");
        } else {
            for (int i = 0; i < taariikhda.size(); i++) {
                System.out.println((i + 1) + ". " + taariikhda.get(i));
            }
 }
}
}
