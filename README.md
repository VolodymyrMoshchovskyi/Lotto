# Lotto
import java.util.Random;
import java.util.Scanner;

public class Lotto {

	public static void main(String[] args) {
		//krok 1 - otrymaty wwedennia wid korystuwacha
		String[] chyslaVidKorystuvacha = OtrymatyVvedenniaVidKorystuvacha();

		int iKilkistSpivpadin = 0;
		int iKilkistRozigrashiv = 0;
		while(iKilkistSpivpadin!=6)
		{
			iKilkistRozigrashiv++;
			//krok 2 - prowesty rozigrash
			int[] tsejRozigrash = ProvestyRozigrash();
			//krok 3 - pereviryty
			iKilkistSpivpadin = PerevirytyRezultat(chyslaVidKorystuvacha, tsejRozigrash);

			if (iKilkistSpivpadin>4)
			{
				//Krok 4 Wywesty rezultat		
				String vsiChyslaRozigrashu = KonvertuvatyMasyvVTekst(tsejRozigrash);

				System.out.println("W "+ iKilkistRozigrashiv+ " loterii spivpaly ("+ vsiChyslaRozigrashu +") "  + iKilkistSpivpadin);
			}
		}

	}
	
	public static String[] OtrymatyVvedenniaVidKorystuvacha()
	{
		System.out.println("Wprowadz 6 czysel z przecinkiem (od 1 do 54): ");
		Scanner scan = new Scanner(System.in);
		String chysla = scan.nextLine();
		scan.close(); 
		String[] strMasyvVvedenychChysel = chysla.split(",");	

		return strMasyvVvedenychChysel;
	}

	public static int[] ProvestyRozigrash()
	{
		int[] tsejRozigrash = new int[6];
		Random r = new Random();
		int iChysloRozigrashu = 0;
		while (iChysloRozigrashu!=6)
		{
			boolean chysloVzheIsnuje = false;
			int tseChyslo = r.nextInt(54)+1;
			for (int isnujucheChyslo: tsejRozigrash)
			{
				if (isnujucheChyslo==tseChyslo)
				{
					chysloVzheIsnuje = true;
					break;
				}
			}
			if (chysloVzheIsnuje!=true)
			{

				tsejRozigrash[iChysloRozigrashu++] = tseChyslo;
			}
		}
		return tsejRozigrash;
	}

	public static int PerevirytyRezultat(String[] strMasyvVvedenychChysel, int[] tsejRozigrash)
	{	
		int iKilkistSpivpadin = 0;
		for (int k=0; k < strMasyvVvedenychChysel.length; k++)
		{
			int chyslo = Integer.parseInt(strMasyvVvedenychChysel[k]);
			for (int tseVygrashneChyslo: tsejRozigrash)
			{
				if (chyslo == tseVygrashneChyslo)
				{
					iKilkistSpivpadin++;
				}
			}
		}
		return iKilkistSpivpadin;
	}

	public static String KonvertuvatyMasyvVTekst(int[] chysla)
	{
		String vsiChyslaRozigrashu = "";
		for (int Chyslo: chysla)
		{
			vsiChyslaRozigrashu = vsiChyslaRozigrashu + Chyslo + " ";
		}
		return vsiChyslaRozigrashu;
	}
}
