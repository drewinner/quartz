
## quartz for golang
quick start:

* cd $GOPATH
* go get github.com/shotdog/quartz
*  code 

```go
  package main
  
  import (
  	"quartz"
  	"log"
  )
  
  var ch chan  int = make(chan int)
  
  func main() {
  
  	qz := quartz.New()
  	job:= quartz.Job{Id:1,
  		Name:"测试Job",
  		Group:"测试",
  		Url:"http://localhost:8080/jobs/**",
  		Params:"参数",
  		Expression:"0 0/10 * * * ?",
  	}
  	err := qz.AddJob(job)
  	if err != nil {
  		log.Panicln(err)
  	}
  
  	job.Name = "修改后job"
  	job.Expression = "0 0/2 * * * ?"
  	err = qz.ModifyJob(job)
  	if err != nil {
  		log.Panicln(err)
  	}
  
  	err = qz.RemoveJob(job.Id)
  	if err != nil {
  		log.Panicln(err)
  	}
  	qz.BootStrap()
  	
  	<-ch
  
  
  }
  // invoke the job 
  func InvokeJob(jobId int ,targetUrl ,params string,nextTime time.Time)  {
  
  	log.Println("jobId=",jobId," targetUrl=",targetUrl," params=",params ," nextTime=",nextTime)
  }

```
