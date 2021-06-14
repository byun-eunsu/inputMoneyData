# inputMoneyData
public class inputMoneyData extends Check implements Serializable {

	private int income;
	private int expenditure;
	private int currentAsset;

	int [] category = {1,2,3,4,5,6,7};
	
	
	public void setIncome(int newIncome) { //수입 설정//
		income = newIncome;
	}
	public void setExpenditure(int newExpenditure) { //지출 설정//
		expenditure = newExpenditure;
	}

	public void setCategoryFood(int newCategoryFood) { //식비 설정//
		category[0] = newCategoryFood; 
	}
	
	public void setCategoryTransportation(int newCategoryTransportation) { //교통비 설정 //
		category[1] = newCategoryTransportation; 
	}
	
	public void setCategoryLeisure(int newCategoryLeisure) { //여가비 설정//
		category[2] = newCategoryLeisure; 
	}
	
	public void setCategoryCommunication(int newCategoryCommunication) { //통신비 설정//
		category[3] = newCategoryCommunication; 
	}
	
	public void setCategoryMedical(int newCategoryMedical) { //의료비 설정//
		category[4] = newCategoryMedical; 
	}
	
	public void setCategoryLifeCost(int newCategoryLifeCost) { //생활비 설정//
		category[5] = newCategoryLifeCost; 
	}
	
	public void setCategoryEtc(int newCategoryEtc) { //기타비 설정//
		category[6] = newCategoryEtc; 
	}
	
	public int getIncome() { 
		return this.income;
	}
	
	public int getExpenditure() {
		return this.expenditure ;
	}
	
	public int getcurrentAsset() { //순수익 (수입 - 지출)  //
		
		return 	currentAsset = income - expenditure;
	}
	
	public int getCategoryFood() { //식비 //
		return category[0];
	}
	
	public int getCategoryTransportation() { //교통비 //
		return category[1]; 
	}
	
	public int getCategoryLeisure() { //여가비//
		return category[2];
	}
	
	public int getCategoryCommunication() { //통신비 //
		return category[3];
	}
	
	public int getCategoryMedical() { //의료비 //
		return category[4];
	}
	
	public int getCategoryLifeCost() { //생활비 //
		return category[5];
	}
	
	public int getCategoryEtc() { //기타비 //
		return category[6];
	}
	
	public void resetCurrentAssetIncome (String addIncome) { //추가 수입 설정//
		
		int addIncomeMoney = Integer.parseInt(addIncome);
		
		if (addIncomeMoney > 0) {
		currentAsset = currentAsset + addIncomeMoney;
		}
		else {
			System.out.println("please enter again range(1 ~ 7) : ");
		}
	}
	
	public void calEachCategoryTotal(String addExpenditure, String categoryNum) { //각 카테고리별 추가 지출계산 method //
		
		int addExpenditureMoney = Integer.parseInt(addExpenditure);
		int categoryNumber = Integer.parseInt(categoryNum);
		
		if (addExpenditureMoney > 0) {
			currentAsset = currentAsset - addExpenditureMoney; //추가 지출 빼기//
			
			if (categoryNumber == 1) {
				category[0] = category[0] - addExpenditureMoney;  //식비 추가 지출 //
				}
			else if (categoryNumber == 2) {
				category[1] = category[1] - addExpenditureMoney; //교통비 추가 지출 //
				}
			else if (categoryNumber == 3) {
				category[2] = category[2] - addExpenditureMoney; //여가비 추가 지출//
				}
			else if (categoryNumber == 4) {
				category[3] = category[3] - addExpenditureMoney; //통신비 추가 지출//
				}
			else if (categoryNumber == 5) {
				category[4] = category[4] - addExpenditureMoney; //의료비 추가 지출//
				}
			else if (categoryNumber == 6) {
				category[5] = category[5] - addExpenditureMoney; //생활비 추가 지출//
				}
			else if (categoryNumber == 7) {
				category[6] = category[6] - addExpenditureMoney;//기타비 추가 지출 //
				}
			else {
				System.out.println("please enter again range(1 ~ 7) : "); //오류 메세지 출력//
			}
			
	}				
}
	
	public static void main(String[] args) throws ClassNotFoundException {
		
		File fileName1 = new File("InputMoneyData.txt"); //이번달 수입지출 파일//
		File fileName2 = new File("lastMonthData.txt"); //저번달 수입지출 파일//

		try {
				ObjectOutputStream thisOutputStream = new ObjectOutputStream(new FileOutputStream (fileName1));//이번달 지출내역 입력//
				inputMoneyData money = new inputMoneyData(); //이번달 지출내역 초기 설정//
				money.setIncome(600000); //수입//
				money.setExpenditure(350000); //지출//
				money.setCategoryFood(70000); //식비//
				money.setCategoryTransportation(50000);//교통비//
				money.setCategoryLeisure(50000); //여가비//
				money.setCategoryCommunication(70000); //통신비//
				money.setCategoryMedical(10000); //의료비//
				money.setCategoryLifeCost(60000); //생활비//
				money.setCategoryEtc(40000); //기타 비용//
				thisOutputStream.writeObject(money);
				thisOutputStream.flush();
				
				ObjectInputStream thisInputStream = new ObjectInputStream(new FileInputStream (fileName1)); 
				inputMoneyData thisMonthOut = (inputMoneyData)thisInputStream.readObject(); //이번달 지출내역 출력//
				System.out.println("Income: " + thisMonthOut.getIncome()); 
				System.out.println("Expenditure: " + thisMonthOut.getExpenditure()); 
				System.out.println("net profit: " + thisMonthOut.getcurrentAsset()); //순수익//
				System.out.println("Food: " + thisMonthOut.getCategoryFood());
				System.out.println("Transportation: " + thisMonthOut.getCategoryTransportation());
				System.out.println("Leisure: " + thisMonthOut.getCategoryLeisure());
				System.out.println("Communication: " + thisMonthOut.getCategoryCommunication());
				System.out.println("Medical: " + thisMonthOut.getCategoryMedical());
				System.out.println("LifeCost: " + thisMonthOut.getCategoryLifeCost());
				System.out.println("Etc: " + thisMonthOut.getCategoryEtc());			
				thisOutputStream.close(); thisInputStream.close();
				
				ObjectOutputStream lastOutputStream = new ObjectOutputStream(new FileOutputStream (fileName2));		
				inputMoneyData lastMonth = new inputMoneyData(); //저번달 지출내역 초기 설정//
				lastMonth.setIncome(600000); //수입//
				lastMonth.setExpenditure(450000); //지출//
				lastMonth.setCategoryFood(80000); //식비//
				lastMonth.setCategoryTransportation(50000); //교통비//
				lastMonth.setCategoryLeisure(80000);//여가비//
				lastMonth.setCategoryCommunication(70000);//통신비//
				lastMonth.setCategoryMedical(50000); //의료비//
				lastMonth.setCategoryLifeCost(80000); //생활비//
				lastMonth.setCategoryEtc(40000); //기타비용//
				lastOutputStream.writeObject(lastMonth);
				lastOutputStream.flush();
				
				ObjectInputStream lastInputStream = new ObjectInputStream(new FileInputStream (fileName2)); //저번달 지출내역 출력//
				inputMoneyData lastMonthOut = (inputMoneyData)lastInputStream.readObject();
				System.out.println("Income: " + lastMonthOut.getIncome());
				System.out.println("Expenditure: " + lastMonthOut.getExpenditure());
				System.out.println("Net profit:" + lastMonthOut.getcurrentAsset());
				System.out.println("Food: " + lastMonthOut.getCategoryFood());
				System.out.println("Transportation: " + lastMonthOut.getCategoryTransportation());
				System.out.println("Leisure: " + lastMonthOut.getCategoryLeisure());
				System.out.println("Communication: " + lastMonthOut.getCategoryCommunication());
				System.out.println("CategoryMedical: " + lastMonthOut.getCategoryMedical()); 
				System.out.println("LifeCost: " + lastMonthOut.getCategoryLifeCost());
				System.out.println("Etc: " + lastMonthOut.getCategoryEtc());
				
				lastOutputStream.close(); lastInputStream.close(); //파일 close //
				
		}
	
		catch (IOException e) {
			System.out.println("Error opening the file ");
			e.printStackTrace();
			System.exit(0);
		}	
		catch (ClassNotFoundException e) {
			System.out.println("Error");
			 e.printStackTrace();
			System.exit(0);
		}	
		
	}

}
