/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package com.jobs;

import com.jobs.SendMail;
import com.reports.SyncReceiptAccount;
import dbcall.CallDBQuery;
import java.util.TimeZone;
import org.quartz.CronExpression;
import org.quartz.CronScheduleBuilder;
import org.quartz.JobBuilder;
import org.quartz.JobDetail;
import org.quartz.Scheduler;
import org.quartz.SimpleScheduleBuilder;
import org.quartz.Trigger;
import org.quartz.TriggerBuilder;
import org.quartz.impl.StdSchedulerFactory;

/**
 *
 * @author Ibrahim
 */
public class JobScheduler {

    
    public void unsubmitLrReportrTrigger(Boolean stop) {
        try {
            String setTime = CallDBQuery.getDetailsForUnsubmitLRJob("TIME");
            JobDetail jb = JobBuilder.newJob(UnsubmitLeaveResumptionMail.class)
                    .withIdentity("jb", "gp").build();

            Trigger trigger2 = TriggerBuilder.newTrigger()
                    .withIdentity("cronTrigger2", "gp")
//                    .withSchedule(CronScheduleBuilder.cronSchedule("0 0/3 * * * ?"))
//                      .withSchedule(CronScheduleBuilder.cronSchedule("0 0 11/1 ? * *").inTimeZone(TimeZone.getTimeZone("Asia/Calcutta")))
                    .withSchedule(CronScheduleBuilder.cronSchedule(setTime).inTimeZone(TimeZone.getTimeZone("Asia/Calcutta")))
//                    .withSchedule(CronScheduleBuilder.cronSchedule("0 30 15 ? * MON").inTimeZone(TimeZone.getTimeZone("Asia/Calcutta")))
//                    .withSchedule(CronScheduleBuilder.cronSchedule("0 0/20 18 * * ? "))
//                    .withSchedule(CronScheduleBuilder.cronSchedule("0 0,15,30,45 14,15,16 ? * * *"))
                    .build();


            Scheduler scheduler2 = new StdSchedulerFactory().getScheduler();
            if (stop) {
                scheduler2.shutdown();
            }
            scheduler2.start();
            scheduler2.scheduleJob(jb, trigger2); 

        } catch (Exception e) {
            e.printStackTrace();
        }
    }       
   
}
