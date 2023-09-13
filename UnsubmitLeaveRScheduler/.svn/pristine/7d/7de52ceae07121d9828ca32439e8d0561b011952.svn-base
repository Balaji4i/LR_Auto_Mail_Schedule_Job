/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package com.jobs;
import com.html.ErrorStatusHTML;
import com.mail.GenericSendMail;
import com.reports.RTFServices;
//import static com.sun.org.apache.xalan.internal.xsltc.compiler.util.Type.String;
import dbcall.CallDBQuery;
import java.text.SimpleDateFormat;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Date;
import java.util.Properties;
import java.util.logging.Level;
import java.util.logging.Logger;
import javax.activation.DataHandler;
import javax.activation.DataSource;
import javax.mail.Message;
import javax.mail.MessagingException;
import javax.mail.BodyPart;
import javax.mail.internet.MimeBodyPart;
import javax.mail.internet.MimeMessage;
import javax.mail.internet.MimeMultipart;
import javax.mail.Multipart;
import javax.mail.PasswordAuthentication;
import javax.mail.Session;
import javax.mail.Transport;
import javax.mail.internet.AddressException;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeMessage;
import org.quartz.Job;
import org.quartz.JobExecutionContext;
import org.quartz.JobExecutionException;
import javax.mail.util.ByteArrayDataSource;
/**
 *
 * @author Nandhini
 */
public class UnsubmitLeaveResumptionMail implements Job  {
  //    public String send(Mail mailBody) {
    /**
     *
     * @param job
     * @throws JobExecutionException
     */  
    @Override
    public void execute(JobExecutionContext job) throws JobExecutionException {
        System.out.println("Excute in Leave Resumption !");
        sendUnsubmitLrReport();
//        sendUnitPriceListReportAvailable();
    }
//
    Object mailContent = ErrorStatusHTML.getUnsubmitLrMailBdy();
    //attachment name
//    String projects1 = CallDBQuery.getDetailsForUnsubmitLRJob("PROJECTS-1")==null ?"":CallDBQuery.getDetailsForUnsubmitLRJob("PROJECTS-1").toString();
        
    String attachmentName1 = null;
           
    String xmlData1 = null;
        
    byte[] bytes1 = null;    
    
//    String projId1=CallDBQuery.getDetailsForUnsubmitLRJob("PROJECTS-ID-1")==null?"":CallDBQuery.getDetailsForUnsubmitLRJob("PROJECTS-ID-1").toString();
    
    //
    public String sendUnsubmitLrReport() {

        final String username = "prismalerts@omniyat.com";
        final String password = "Or@cl3alert";
        Properties props = new Properties();
        props.put("mail.smtp.auth", "true");
        props.put("mail.smtp.starttls.enable", "true");
        props.put("mail.smtp.host", "smtp.office365.com");
        props.put("mail.smtp.ssl.protocols", "TLSv1.2");
        props.put("mail.smtp.port", "587");

        String toAddress_all = CallDBQuery.getAddressForUnsubmitLR("TO");
        String ccAddress_all = CallDBQuery.getAddressForUnsubmitLR("CC");
        String bccAddress_all = CallDBQuery.getAddressForUnsubmitLR("BCC");
//        
        
//        String toAddress_all="prasenjit.d@4iapps.com";
//        String ccAddress_all="prasenjit.d@4iapps.com";
//        String bccAddress_all="";

        /**
         * If there is no data in DB it will refer below mails.
//         */
        if ("".equals(toAddress_all)) {
            toAddress_all = "prasenjit.d@4iapps.com";
        }
         if ("".equals(ccAddress_all)) {
            ccAddress_all = "sudha.y@4iapps.com";
        }
        if ("".equals(bccAddress_all)) {
            bccAddress_all = "prasenjit.d@4iapps.com";
        }


        String subject = "Unsubmit Leave Resumption Report on - " + getSysdate("dd-MMM-yyyy");
        String result1 = null;
        String filePath = "/u01/data/report/LeaveResumption/Unsubmitted_LR_EmpList.rtf";
    
//        if(!projects1.equals("")){
         attachmentName1 = "Unsubmitted LR "+getSysdate("dd-MMM-yyyy")+".pdf";
         xmlData1 = CallDBQuery.getUnsubmitLRReport(getSysdate("dd-MMM-yyyy"));
         if("NO_DATA".equals(xmlData1)){ 
            xmlData1 = CallDBQuery.getEmptyUnsubmitLrXml();
            }
          bytes1 = RTFServices.rtfReport(xmlData1, filePath);
//        }        
        
//        if(!projects1.equals("")){ //1 proj
            result1 = GenericSendMail.sendWithMultipleAttachment1(username, password, props, bytes1,toAddress_all, ccAddress_all, bccAddress_all, subject, mailContent,attachmentName1);
//        }       
     
        return result1;
    }         
   
    public String getSysdate(String format) {
        Date date = new Date();
        SimpleDateFormat formatter = new SimpleDateFormat(format);
        String strDate = formatter.format(date);
        return strDate;
    }

    
}



